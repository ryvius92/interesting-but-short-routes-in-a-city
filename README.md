# short-and-interesting-routes-in-a-city

Walking routes planner which try to find interesting but not too long routes - compared to the shortest alternative -  between two chosen points on a city map. <br />
The application is written in Javascript and it's client side only.

<br />

<br />



## How does it work

The are three main parts: <br />

City map and areas <br />
Leaflet and OSM are used to dispay the city map (you are given a choice between Milan and Florence... but more cities map could be added). The map is equally partioned in areas of about 400x250 meters, where each of them represent a possible location to visit. <br /> <br />

Define how a city area is "interesting" <br />
A score is given to each area, and it's calcuated with the stats and metadata of geotagged public Flickr photos such as : total number of photos and views. Part of the score is calculated also by performing a text sentiment analysis on the photos tags (using a score dictionary).
<br /> <br />

Computation of the best route  <br />
How is the route chosen ? the aim is to choose a route where shortness and "interestingness" are balanced. The algorithm is as follows : 


<br />


* Computation of the fastest route (with Mapzen)
* Creation of a list of all areas near the fastest route - the limit is a 1km circle from each point of the route <br /> 
* The list is then ordered by score and filtered applying more distance and scores criteria (example : the score is not high enough) <br /> 
* Selection of 1 or 2 waypoints <br /> The center of the best remaining area is selected as an intermediate point for the new route. A possible second waypoint is searched between the other remaining areas, and it is chosen only if its distance to the first waypoint is  acceptable. <br /> 

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


## What do you need

To run the application you need a mapzen key (a free key is fine as well) and a lickr developer key.

```
router: L.Routing.mapzen('mapzen_key', {costing:'pedestrian'})
```

```
var flickr = new Flickr({
			api_key: "flickr_key"
		});
```

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





