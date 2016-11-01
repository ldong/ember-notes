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

