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


