
<center>
  <h1> Vue Stripe Checkout </h1>
  <span>
    <a href="https://circleci.com/gh/jofftiquez/vue-stripe-checkout" title="Circle CI">
      <img src="https://circleci.com/gh/jofftiquez/vue-stripe-checkout.svg?style=shield" alt="Circle CI"/>
    </a>
  </span><span>
    <a href="https://www.npmjs.com/package/vue-stripe-checkout" title="NPM">
      <img src="https://img.shields.io/npm/dt/vue-stripe-checkout.svg?style=shield" alt="NPM"/>
    </a>
  </span><span class="badge-buymeacoffee">
    <a href="https://www.buymeacoffee.com/jofftiquez" title="Donate to this project using Buy Me A Coffee">
      <img src="https://img.shields.io/badge/buy%20me%20a%20coffee-donate-brightgreen.svg" alt="Buy Me A Coffee donate button"/>
    </a>
  </span>
</center>

# ⚠️ LEGACY VERSION ⚠️

This version of Vue Stripe Checkout is based on Stripe Checkout V2. Stripe is now using Stripe Checkout V3. Development for V3 integration is still ongoing. Kindly refer to [#55](https://github.com/jofftiquez/vue-stripe-checkout/issues/56), [#56](https://github.com/jofftiquez/vue-stripe-checkout/issues/56), and [#64](https://github.com/jofftiquez/vue-stripe-checkout/issues/64) for more information.

# ⚠️ TRY VERSION 3 BETA NOW! ⚠️

- [Branch](https://github.com/jofftiquez/vue-stripe-checkout/tree/refactor/v3)
- [Release](https://github.com/jofftiquez/vue-stripe-checkout/releases/tag/v3.0.0-beta)

---- 

**Shut up and clone my repo!**

A Vue plugin for Stripe checkout. I sh\*t you not, this plugin is the easiest to use. 

### Demo

[Shut up and see the demo!](https://jofftiquez.github.io/vue-stripe-checkout/)

If you liked this repo then leave a :star:, if not, I don't care. *(Seriously leave a :star: please)*

![Screen Shot](https://i.imgur.com/hV6iNj3.png)

## Install

*NPM* or *Yarn*

`npm install vue-stripe-checkout --save`

`yarn add vue-stripe-checkout`

*CDN*

For specific version prior to v3:
`https://unpkg.com/vue-stripe-checkout@1.2.6/build/vue-stripe-checkout.js`

For v3 releases:
`https://unpkg.com/vue-stripe-checkout@3.0.0-beta.11/dist/index.js`

For the newest release:
`https://unpkg.com/vue-stripe-checkout`

*Usage*

```javascript
import Vue from 'vue';
import VueStripeCheckout from 'vue-stripe-checkout';

Vue.use(VueStripeCheckout, 'your-publishable-key-here');
```

Just see the [stripe docu](https://stripe.com/docs/checkout#integration-simple-options) for all of the available options.

### Sample

```vue
<template>
  <div>
    <vue-stripe-checkout
      ref="checkoutRef"
      :image="image"
      :name="name"
      :description="description"
      :currency="currency"
      :amount="amount"
      :allow-remember-me="false"
      @done="done"
      @opened="opened"
      @closed="closed"
      @canceled="canceled"
    ></vue-stripe-checkout>
    <button @click="checkout">Checkout</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      image: 'https://i.imgur.com/HhqxVCW.jpg',
      name: 'Shut up and take my money!',
      description: 'Cats are the best dog!',
      currency: 'PHP',
      amount: 99999
    }
  },
  methods: {
    async checkout () {
      // token - is the token object
      // args - is an object containing the billing and shipping address if enabled
      const { token, args } = await this.$refs.checkoutRef.open();
    },
    done ({token, args}) {
      // token - is the token object
      // args - is an object containing the billing and shipping address if enabled
      // do stuff...
    },
    opened () {
      // do stuff 
    },
    closed () {
      // do stuff 
    },
    canceled () {
      // do stuff 
    }
  }
}
</script>
```

### Props

See property description from official [Stripe Documentation](https://stripe.com/docs/checkout#highly-recommended)

- `publishable-key`: `String`
- `image`: `String`
- `name`: `String`
- `description`: `String`
- `amount`: `Number`
- `locale`: `String`
- `zip-code`: `Boolean`
- `billing-address`: `Boolean`
- `currency`: `String`
- `panelLabel`: `String`
- `shipping-address`: `Boolean`
- `email`: `String`
- `allow-remember-me`: `Boolean`
- `auto-open-modal`: `Boolean`

### Events

- `done` - Emits an object containing the stripe `token` and `args` (an object containing the billing and shipping address if enabled).
- `opened` - Called when the stripe checkout dialog has been opened.
- `closed` - Called when the stripe checkout dialog has been closed after a successful transaction or when the x button was clicked.
- `canceled` - Called when x button has been clicked.

**Usage**

```vue
<vue-stripe-checkout
  @done="done"
  @opened="opened"
  @closed="closed"
  @canceled="canceled"
></vue-stripe-checkout>
```

**SPECIAL THANKS TO THE FOLLOWING SPONSOR(S):**

[<img src="https://i.imgur.com/Ttv4fMw.png" width="200px">](https://mightyminds.org)
[<img src="https://i.imgur.com/x0SERyj.png" width="200px">](https://mycure.md)
[<img src="https://i.imgur.com/4jF5M4A.png">](http://myteamops.com)

Made with :heart: by Jofferson Ramirez Tiquez
