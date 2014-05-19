# FIXED
## utils.js

### offset

```js
	me.offset = function (el) {
		return {
	 		left: el.getBoundingClientRect().left * -1,
	 		top: el.getBoundingClientRect().top * -1
	  		};
	}
```

## zoom.js

### _wheelZoom

```js
	_wheelZoom: function (e) {
		var wheelDeltaY,
			deltaScale,
			that = this;

		// Execute the zoomEnd event after 400ms the wheel stopped scrolling
		clearTimeout(this.wheelTimeout);
		this.wheelTimeout = setTimeout(function () {
			that._execEvent('zoomEnd');
		}, 400);

		if ( 'deltaX' in e ) {
			wheelDeltaY = -e.deltaY / Math.abs(e.deltaY);
		} else if ('wheelDeltaX' in e) {
			wheelDeltaY = e.wheelDeltaY / Math.abs(e.wheelDeltaY);
		} else if('wheelDelta' in e) {
			wheelDeltaY = e.wheelDelta / Math.abs(e.wheelDelta);
		} else if ('detail' in e) {
			wheelDeltaY = -e.detail / Math.abs(e.wheelDelta);
		} else {
			return;
		}

		// BugFix, a volte ritorna NaN e blocca lo zoom
		if ( !wheelDeltaY || wheelDeltaY == NaN ) wheelDeltaY = 0;

		deltaScale = this.scale + wheelDeltaY / 5;

		this.zoom(deltaScale, e.pageX, e.pageY, 0);
	},
```
