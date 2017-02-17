# short-and-interesting-routes-in-a-city
Urban walking routes planner capable of selecting interesting but not overly long routes (compared to the shortest alternative) between a start and a destination point chosen by the user. <br />
The metadata of all geotagged Flickr photos inside a city have been used for the creation of a city’s areas ranking.

<br />

<br />



## How to use

Insert your mapzen free key inside the codE (html file) where the routes are initialized.

```
router: L.Routing.mapzen('mapzen_key', {costing:'pedestrian'})
```

Insert your Flickr developer api key in the Flickr code section.

```
var flickr = new Flickr({
			api_key: "flickr_key"
		});
```

<br />

<br />

## How does it work

The control flow of the application can be partitioned into three main parts. <br />
First the city’s map is created with Leaflet and with OSM standard map as layer, then it is separated in small and equal cells of about 400x250 meters, where each of them represent a possible interesting location to visit. <br />
As an example, the central area of Milan is partioned into a grid of 228 small areas. <br />
The second part of the application is about calculating a score expressing the interestingness of each area. <br />
With asynchronus calls to Flickr, the metadata of all the geotagged photos which belongs to the city are downloaded. Each answer from Flickr return a list of 250 photos, so the request is reiterated many times. <br />
After the extraction of the most important statistics about the photos (coordinates, number of visualizations, tags), the score of each area is calculated by combaining two different type of inputs: <br />

* a score expressing some numeric metadata of all the geotagged photos inside the area, such as total number of photos and total number of views
* a score expressing the index of pleasantness of the area, obtained by executing a Text Sentiment Analysis on the photos tags.

<br />

The last part of the program is about the research of the most interesting areas and the creation of the new alternative route. The most important instructions are:

* Computation of the fastest route (with the routing service Mapzen)
* Creation of a list of all areas <br />All areas whose center is inside a 1 km circle from every point of the fastest route are added to a list, which is then ordered in a desc order by the score.
* Reduction of the area’s list<br /> Several controls about the distance between the center of each area and the start and destination points have been applied. Those areas who exceed the distance’s limit are excluded from the list.
* Selection of 1 or 2 waypoints <br />The center of the best remaining area is selected as an intermediate point for the new route. A possible second waypoint is searched between the other areas, and it is chosen only if its distance with the first waypoint is acceptable. <br /> The new route (calculated with Mapzen) try to represent the best possible combination between shortness and interestingness.

<br />

<br />

## Examples

Example of the route planner in a mobile app environment. <br />
The red route is the shortest one, the blue one is the 'most interesting' route, with two interesting areas crossed.

<br />

![alt tag](https://github.com/ryvius92/short-and-interesting-routes-in-a-city/blob/master/percorso.jpg)

<br />

Routes Statistics :




<br />

<br />


## Acknowledgments

* [Leaflet](http://leafletjs.com/)
* [Leaflet Routing Machine](https://github.com/perliedman/leaflet-routing-machine)
* [LRM-Mapzen](https://github.com/mapzen/lrm-mapzen)
* [Turf](https://github.com/Turfjs/turf)
* [Flickrapi](https://github.com/Pomax/node-flickrapi)
* [Sentiment-Multilang](https://github.com/davidemiceli/sentiment-multilang)
* ['The Shortest Path to Happiness'](https://arxiv.org/abs/1407.1031)





