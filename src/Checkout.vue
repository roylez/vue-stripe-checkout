<template>
  <div>
    <slot name="checkout-button" />
  </div>
</template>

<script>
import { 
  SUPPORTED_LANGS,
  SUPPORTED_SUBMIT_TYPES,
  BILLING_ADDRESS_COLLECTION_TYPES
} from './contants';
export default {
  props: {
    items: {
      type: Array
    },
    successUrl: {
      type: String,
      default: window.location.href
    },
    cancelUrl: {
      type: String,
      default: window.location.href
    },
    submitType: {
      type: String,
      default: 'auto',
      validator: (value) => SUPPORTED_SUBMIT_TYPES.includes(value)
    },
    billingAddressCollection: {
      type: String,
      default: 'auto',
      validator: (value) => BILLING_ADDRESS_COLLECTION_TYPES.includes(value)
    },
    clientReferenceId: {
      type: String,
    },
    customerEmail: {
      type: String
    },
    sessionId: {
      type: String
    },
    locale: {
      type: String,
      default: 'auto',
      validator: (value) => SUPPORTED_LANGS.includes(value)
    }
  },
  methods: {
    redirectToCheckout () {
      try {
        var opts = {
          billingAddressCollection: this.billingAddressCollection,
          cancelUrl: this.cancelUrl,
          clientReferenceId: this.clientReferenceId,
          customerEmail: this.customerEmail,
          items: this.items,
          locale: this.locale,
          sessionId: this.sessionId,
          submitType: this.submitType,
          successUrl: this.successUrl,
        }
        opts.items[0].plan && delete opts.submitType
        this.$emit('loading', true);
        this.$stripe.redirectToCheckout(opts);
      } catch (e) {
        console.error(e);
        this.$emit('error', e);
      } finally {
        this.$emit('loading', false);
      }
    }
  }
}
</script>
