# short-and-interesting-routes-in-a-city

Walking routes planner which try to find interesting but not too long routes - compared to the shortest alternative -  between two chosen point on a city map. <br />
The application is written in Javascript and it's client side only.

<br />

<br />



## How to use  - and what do you need

The application need a mapzen key (a free key is fine as well) :

```
router: L.Routing.mapzen('mapzen_key', {costing:'pedestrian'})
```

You'll also need to insert your Flickr developer api key right here :

```
var flickr = new Flickr({
			api_key: "flickr_key"
		});
```

<br />

<br />

## How does it work

The are three main parts. <br />

- Use of a map and definition of city area. <br />
Leaflet and OSM are used to dispay the city map (you are given a choice between Milan and Florence... but more cities can be easily added). The map is partioned in small and equal cells of about 400x250 meters, where each of them represent a possible location to visit. <br />

- Define how an area is "interesting" <br />
Flickr photos metadata are used to calculate a score for each area combining statisics such as : total number of photos, views and a text sentiment analysis on the photos tags (using a score dictionary).

- Computation of the best route  <br />
How is the route chosen ? the aim is to choose a route where shortness and "interestingness" are balanced. The algorithm is as follows : 

* Computation of the fastest route (with Mapzen)
* Creation of a list of all areas near the fastest route (the limit is a 1km circle from each point of the route) <br /> 
* The list is then ordered by score <br /> 
* List of areas is then filtered more. Areas that are too far or have a not enough high score are removed (see the code for more details):
* Selection of 1 or 2 waypoints <br /> The center of the best remaining area is selected as an intermediate point for the new route. A possible second waypoint is searched between the other areas, and it is chosen only if its distance with the first waypoint is considered acceptable. <br /> 

<br />

<br />

## Examples (Milan)

The red route is the shortest one, the blue one is the 'most interesting' route, with two interesting areas crossed.

<br />

![alt tag](https://github.com/ryvius92/short-and-interesting-routes-in-a-city/blob/master/percorso.jpg) ![alt tag](https://github.com/ryvius92/short-and-interesting-routes-in-a-city/blob/master/istruzioni_percorso.jpg)

<br />

Routes Statistics :

![alt tag](https://github.com/ryvius92/short-and-interesting-routes-in-a-city/blob/master/valutazione1.jpg)




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





