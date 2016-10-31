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
