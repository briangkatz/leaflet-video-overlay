# Embed a video onto a Leaflet map

#### [Demo](https://briangkatz.github.io/leaflet-video-overlay)

``` javascript
// Set the bounds of the map where you want the video to display
var videoBounds = L.latLngBounds([[ 50, -170], [ 30, -130]]);

// Create a rectangle overlay at the bounds you set
L.rectangle(videoBounds).addTo(mymap);

// Link your video
var videoUrls = [
    'video/airplane.mp4'
];

// Create the overlay to show your video at the bounds you set
var videoOverlay = L.videoOverlay( videoUrls, bounds, {
    opacity: 1
}).addTo(mymap);

// Add the video overlay to the map with pause and play buttons
videoOverlay.on('load', function () {
    var MyPauseControl = L.Control.extend({
        onAdd: function() {
            var button = L.DomUtil.create('button');
            button.innerHTML = '⏸';
            L.DomEvent.on(button, 'click', function () {
                videoOverlay.getElement().pause();
            });
            return button;
        }
    });
    var MyPlayControl = L.Control.extend({
        onAdd: function() {
            var button = L.DomUtil.create('button');
            button.innerHTML = '⏵';
            L.DomEvent.on(button, 'click', function () {
                videoOverlay.getElement().play();
            });
            return button;
        }
    });
    var pauseControl = (new MyPauseControl()).addTo(mymap);
    var playControl = (new MyPlayControl()).addTo(mymap);
});
```



