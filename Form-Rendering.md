#### Creating a New Document (Doc)

1. Route is set to `app.html#Form/[DOCTYPE]/New DOCTYPE 1`.
1. Browser fires the `hashchange` event.
1. `haschange` is bound in `router.js` to call `wn.route` method.
1. Recognising that it is a Form which we are trying to open, `wn.route` calls `wn.views.formview.show`
1. `formview.show` creates a new `_f.Frm` object, changes the container to point to this new form and calls its refresh method
1. `refresh` method of the form object calls `setnewdoc`
1. Then, Following events are fired in sequence:
    1. `cur_frm.cscript.onload` (only for new)
    1. `cur_frm.cscript.refresh`
    1. `cur_frm.cscript.onload_post_render` (only for new)