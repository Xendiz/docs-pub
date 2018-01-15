# Xendiz Cookie Sync service

### Cookie Syncing with Xendiz DSP
Xendiz provides a html sync code that should be loaded into the browser on impression
```html
iframe (recomended):
<iframe src="https://advsync.com/xendiz/ssp/?location=REDIRECT_URL" style="display:none"></iframe>
pixel: 
<img src="https://advsync.com/xendiz/ssp/?pixel=1&location=REDIRECT_URL" style="display:none">
```
Where `REDIRECT_URL` is url-encoded SSP sync endpoint. `REDIRECT_URL` must include macro {UID} which will be replaced by actual `user id`.
When sending requests to the Xendiz, `user id` should be passed in `user.buyerid` object.

### Cookie Syncing with Xendiz SSP
Xendiz provides a sync url with a unique `:id` to the DSP.
```
iframe (recomended): https://advsync.com/xendiz/dsp/:id/?buid={UID}
pixel: https://advsync.com/xendiz/dsp/:id/?pixel=1&buid={UID} 
```
DSP should redirect to this url after replacing the macro {UID} with actual `user id`.
DSP should provide cookie sync code which will be loaded on impression.
Xendiz will pass DSP's `user id` in `user.buyerid` object.
