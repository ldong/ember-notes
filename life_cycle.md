# Ember Life Cycle

## Route

```javascript
export default Ember.Route.extend({
  init: function() {
    // this._super(...arguments);
    console.log('controller');
  },

  renderTemplate() {
    console.log('renderTemplate');
  },

  beforeModel(transition){
    console.log('beforeModel');
  },

  afterModel(transition) {
    console.log('afterModel');
  },

  setupController(controller, model) {
    console.log('setupController');
  },

  activate() {
    console.log('activate');
  },

  deactivate() {
    console.log('deactivate');
  },

  actions: {
    didTransition() {
      console.log('didTransition');
      return true; // Bubble the didTransition event
    },

    willTransition(transition) {
      console.log('willTransition');
    }
  }
})
```

Ref: http://ember.vicramon.com/ember-route

## Controller

```javascript
export default Ember.Controller.extend({
  didUpdateAttrs(){
    console.log('didUpdateAttrs');
  },

  didReceiveAttrs(){
    console.log('didReceiveAttrs');
  },

  willRender() {
    console.log('before render administration');
  },

  didUpdate() {
    console.log('did update');
  },

  didRender() {
    console.log('did Render');
  }
});
```

## Components

```javascript
import Ember from 'ember';

export default Ember.Component.extend({
  didInitAttrs(options) {
    console.log('didInitAttrs', options);
  },

  didUpdateAttrs(options) {
    console.log('didUpdateAttrs', options);
  },

  willUpdate(options) {
    console.log('willUpdate', options);
  },

  didReceiveAttrs(options) {
    console.log('didReceiveAttrs', options);
  },

  willRender() {
    console.log('willRender');
  },

  didRender() {
    console.log('didRender');
  },

  didInsertElement() {
    console.log('didInsertElement');
  },

  didUpdate(options) {
    console.log('didUpdate', options);
  },
});
```

Ref:

1. https://gist.github.com/jpadilla/2f9d698cdaed87821623
2. https://github.com/emberjs/ember.js/blob/v2.8.2/packages/ember-htmlbars/lib/component.js#L413
