# Ember Notes

Some tips I learn along the way

## Routes

When transitioning between routes, the Ember router collects all of the models
(via the model hook) that will be passed to the route's controllers at the end
of the transition. If the model hook (or the related beforeModel or afterModel
hooks) return normal (non-promise) objects or arrays, the transition will
complete immediately. But if the model hook (or the related beforeModel or
afterModel hooks) returns a promise (or if a promise was provided as an
argument to transitionTo), the transition will pause until that promise
fulfills or rejects.


https://guides.emberjs.com/v1.10.0/routing/asynchronous-routing/


## RESTSerializer

```
import Ember from 'ember';
import DS from 'ember-data';

export default DS.RESTSerializer.extend({
  // normalize (modelClass, resourceHash, prop) {
  //   console.log('run normalize');
  // },

  /**
   * normalize the payload for the filters response
   * @param  {DS.Store} store             main store
   * @param  {DS.Model} primaryModelClass model type
   * @param  {Obejct} payload             response from server
   * @param  {String|Number} id           id requested, should be null
   * @param  {String} requestType         type of request, findAll, findRecord
   * @return {Object}                     JSON-API document
   */
  normalizeResponse(store, primaryModelClass, payload, id, requestType) {
    console.log('run normalizeResponse');
    // return this._super(store, primaryModelClass, payload, id, requestType);

    // let newPayload = [];
    // payload.forEach((mdms, id) => {
    //   newPayload.push({
    //     mdms: mdms
    //   });
    // });

    // payload.forEach(item => {
    //   item.id = item.mdm.id;
    // });

    let newPayload = {
      mdms: payload
    };
    console.log('newPayload', newPayload);

//     newPayload = {
//   "mdms": [
//     {
//       "mdm": {
//         "id": 18,
//         "mdmKey": 11145123,
//         "customHeader": "test added something",
//         "imgUrl": "test.com",
//         "description": "test",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": "adong@yahoo-inc.com"
//       },
//       "tier": {
//         "id": 4,
//         "name": "GOLD",
//         "isInternal": false,
//         "description": null,
//         "createdBy": "sdu@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "regions": [
//         {
//           "id": 21,
//           "name": "UK",
//           "woeid": "23424975",
//           "description": "United Kingdom",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         }
//       ],
//       "id": 18
//     },
//     {
//       "mdm": {
//         "id": 19,
//         "mdmKey": 222,
//         "customHeader": "abc",
//         "imgUrl": "logo",
//         "description": "comment",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "tier": {
//         "id": 4,
//         "name": "GOLD",
//         "isInternal": false,
//         "description": null,
//         "createdBy": "sdu@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "regions": [
//         {
//           "id": 11,
//           "name": "US",
//           "woeid": "23424977",
//           "description": "United States",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         }
//       ],
//       "id": 19
//     },
//     {
//       "mdm": {
//         "id": 21,
//         "mdmKey": 333,
//         "customHeader": "custom header",
//         "imgUrl": "http://some.com/logo.png",
//         "description": "comment",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "id": 21
//     },
//     {
//       "mdm": {
//         "id": 24,
//         "mdmKey": 1111111,
//         "customHeader": "some header title",
//         "imgUrl": "http://yahoo.com/logo.png",
//         "description": "ccccc",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "tier": {
//         "id": 4,
//         "name": "GOLD",
//         "isInternal": false,
//         "description": null,
//         "createdBy": "sdu@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "regions": [
//         {
//           "id": 11,
//           "name": "US",
//           "woeid": "23424977",
//           "description": "United States",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         }
//       ],
//       "id": 24
//     },
//     {
//       "mdm": {
//         "id": 25,
//         "mdmKey": 2222222,
//         "customHeader": "some header name",
//         "imgUrl": "http://yahoo.com/oldversion.png",
//         "description": "",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "tier": {
//         "id": 4,
//         "name": "GOLD",
//         "isInternal": false,
//         "description": null,
//         "createdBy": "sdu@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "regions": [
//         {
//           "id": 21,
//           "name": "UK",
//           "woeid": "23424975",
//           "description": "United Kingdom",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         },
//         {
//           "id": 11,
//           "name": "US",
//           "woeid": "23424977",
//           "description": "United States",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         }
//       ],
//       "id": 25
//     },
//     {
//       "mdm": {
//         "id": 26,
//         "mdmKey": 555555,
//         "customHeader": "some string",
//         "imgUrl": "http://abc.com/xyz.png",
//         "description": "",
//         "createdBy": "adong@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "tier": {
//         "id": 5,
//         "name": "SILVER",
//         "isInternal": false,
//         "description": null,
//         "createdBy": "sdu@yahoo-inc.com",
//         "updatedBy": null
//       },
//       "regions": [
//         {
//           "id": 19,
//           "name": "CA",
//           "woeid": "23424775",
//           "description": "Canada",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": null
//         },
//         {
//           "id": 22,
//           "name": "TW",
//           "woeid": "23424971",
//           "description": "taiwan",
//           "createdBy": "sdu@yahoo-inc.com",
//           "updatedBy": "sdu@yahoo-inc.com"
//         }
//       ],
//       "id": 26
//     }
//   ]
// }
    // debugger;
    return this._super(store, primaryModelClass, newPayload, id, requestType);
    // return this._super(store, primaryModelClass, payload, id, requestType);
  },

  // normalizeFindAllResponse(store, primaryModelClass, payload, id, requestType){
  //   console.log('normalizeFindAllResponse');
  //   return this._super(store, primaryModelClass, payload, id, requestType);
  // },

  // normalizeArrayResponse (store, primaryModelClass, payload, id, requestType) {
  //   console.log('run normalizeArrayResponse');

  //   return this._super(store, primaryModelClass, payload, id, requestType);
  // },


});
```

## Model

```
import DS from 'ember-data';

export default DS.Model.extend({
  // mdm: DS.belongsTo('mdm'),
  // tier: DS.belongsTo('tier'),
  // regions: DS.hasMany('region')

  mdmKey: DS.attr('number'),
  imgUrl: DS.attr('string'),
  customHeader: DS.attr('string'),
  description: DS.attr('string'),
  createdBy: DS.attr('string'),
  updatedBy: DS.attr('string'),
  tier: DS.attr(),
  regions: DS.attr()


  // regions: DS.attr('', { defaultValue: [] })
  // this.store.find('tier', {id: [1,2,3]});

  // proper way
  // mdm: DS.attr(),
  // tierId: DS.attr('number'),
  // regionIds: DS.attr()


  // id: DS.attr('number'),

  // mdmKey: DS.attr('number'),
  // customHeader: DS.attr('string'),
  // imgUrl: DS.attr('string'),
  // description: DS.attr('string'),
  // createdBy: DS.attr('string'),
  // updatedBy: DS.attr('string')
});

//Tier

// import DS from 'ember-data';

// export default DS.Model.extend({
//   // id: DS.attr('number'),
//   // name: DS.attr('string'),
//   // isInternal: DS.attr('boolean'),
//   // description: DS.attr('string'),
//   // createdBy: DS.attr('string'),
//   // updatedBy: DS.attr('string')
// });


// Region
// import DS from 'ember-data';

// export default DS.Model.extend({

//   // id: DS.attr('number'),

//   // name: DS.attr('string'),
//   // woeid: DS.attr('string'),
//   // createdBy: DS.attr('string'),
//   // updatedBy: DS.attr('string'),

//   // Do we have to use belongsTo? Its good practice to keep it here, not required though
//   // mdms: DS.belongsTo('mdms'),
// });

```


## Mut

Working

```
{{#each tiers as |tier|}}
  <label
    class="btn btn-primary
    {{if (eq mdm.tier tier) "active" ""}}"
    onclick={{action (mut mdm.tier) tier}}
  >
    <input type="radio" name="role">{{tier.name}}
  </label>
{{/each}}

```

Alternative

Handlebars
```
{{#each tiers as |tier|}}
  <label class="btn btn-primary {{if (eq selectedTier tier) "active" ""}}" {{action "updateSelectedTier" tier}}>
    <input type="radio" name="role">{{tier.name}}
  </label>
{{/each}}

```

Controller/ Component.js
```
  actions: {
    updateSelectedTier(tier) {
      console.log('updateSelectedTier', tier);
      this.set('selectedTier', tier);
    }
  }
```
Only works on primities, string, number and boolean, it wont work on `objects`.

Ref: https://til.hashrocket.com/posts/dc22a1be25-lets-talk-about-embers-mut-htmlbars-helper


# Serializer

[javascript closure change parameter](http://javascriptissexy.com/understand-javascript-closures-with-ease/)


```javascript
change = function(a) {
 a = a.data;
}

b = {data: 100}
change(b)
```

### Serializer

```javascript
import Ember from 'ember';
import DS from 'ember-data';

export default DS.RESTSerializer.extend({
  serializeIntoHash: function(data, type, record, options) {
    this._super(...arguments);
    data = data.mdm;

    // var root = Ember.String.decamelize(type.modelName);
    // data[root] = this.serialize(record, options);
    // data = this.serialize(record, options);
  },

  // serializeIntoHash: function(data, type, record, options) {
  //   var root = Ember.String.decamelize(type.modelName);
  //   // data[root] = this.serialize(record, options);
  //   data = this.serialize(record, options);
  //   return data;
  // },

  // serialize(snapshot, options) {
  //   var json = this._super(...arguments);

  //   // json.data.attributes.cost = {
  //   //   amount: json.data.attributes.amount,
  //   //   currency: json.data.attributes.currency
  //   // };

  //   // delete json.data.attributes.amount;
  //   // delete json.data.attributes.currency;

  //   return json;
  // },

  // normalize (modelClass, resourceHash, prop) {
  //   console.log('run normalize');
  // },
  //


  /**
   * normalize the payload for the filters response
   * @param  {DS.Store} store             main store
   * @param  {DS.Model} primaryModelClass model type
   * @param  {Obejct} payload             response from server
   * @param  {String|Number} id           id requested, should be null
   * @param  {String} requestType         type of request, findAll, findRecord
   * @return {Object}                     JSON-API document
   */
  normalizeResponse(store, primaryModelClass, payload, id, requestType) {
    console.log('run normalizeResponse');

    let newPayload = {
      mdms: payload
    };
    console.log('newPayload', newPayload);
    return this._super(store, primaryModelClass, newPayload, id, requestType);
  },

  // normalizeFindAllResponse(store, primaryModelClass, payload, id, requestType){
  //   console.log('normalizeFindAllResponse');
  //   return this._super(store, primaryModelClass, payload, id, requestType);
  // },

  // normalizeArrayResponse (store, primaryModelClass, payload, id, requestType) {
  //   console.log('run normalizeArrayResponse');

  //   return this._super(store, primaryModelClass, payload, id, requestType);
  // },


});
```

### Adapter

```javascript
import BaseAdapter from 'insights/adapters/base-adapter';

/**
 * rest adapter for requesting mdm
 */
export default BaseAdapter.extend({
  // createRecord(store, type, snapshot) {

  //   this._super(...arguments);
  //   // var serializer = store.serializerFor(type.modelName);
  //   // var url = this.buildURL(type.modelName, null, snapshot, 'createRecord');
  //   // let data = serializer.serializeIntoHash(data, type, snapshot, { includeId: true });

  //   // // const data = this.serialize(snapshot);
  //   // return this.ajax(url, "POST", { data: data });
  // },

  /**
   * builds url for the filters from the base
   * @return {String}              complete url
   */
  buildURL() {
    const endpoint = 'mdms';
    const host = this.host();
    const wssid = this.wssid();
    const userId = this.get('authentication.currentUser.email');
    const provider = this.get('provider');

    const url = `${host}/aiy-mw/api/ai_ur/${endpoint}?wssid=${wssid}&provider=${provider}`;

    return url;
  }
});

```


## Model

[javascript - Id is lost while trying to JSON.stringify Ember model - Stack Overflow](http://stackoverflow.com/questions/29513240/id-is-lost-while-trying-to-json-stringify-ember-model)

[ember JSON.stringify without id](ember JSON.stringify without id)


```
You need to pass in the includeId option to the toJSON method in order to get the ID in the JSON.

var plan = this.get('model');
var reqBody = JSON.stringify({
    plan: plan.toJSON({ includeId: true }),
    token
});
Select
And if you didn't know, JSON.stringify() will call toJSON() for you (which is what is happening in your case). If you want to call JSON.stringify() instead of model.toJSON({}), you can always override it:

App.Plan = DS.Model.extend({
    toJSON: function() {
        return this._super({ includeId: true });
    }
});
That way JSON.stringify(plan) will give you exactly what you want.
```


## Ember Closure Actions

```
<input type="text" onchange={{action "logArgs" value="target.value"}}> <!-- Logs the value of the input (e.target.input) -->

<input type="checkbox"
       checked={{isChecked}}
       onclick={{action "foo" value="target.checked"}} />
```

Use `mut`?

actions up, data down.


Ref:

1. http://miguelcamba.com/blog/2016/01/24/ember-closure-actions-in-depth/
2. http://balinterdi.com/2015/09/25/select-in-ember-with-multiple-selection.html
3. https://emberigniter.com/parent-to-children-component-communication/

