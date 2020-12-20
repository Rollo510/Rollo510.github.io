---
layout: post
title:      "PITSTOP: Put your life in danger for free rides!"
date:       2020-12-20 14:46:05 -0500
permalink:  pitstop_put_your_life_in_danger_for_free_rides
---


With the advent of Google Maps, it's never been easier to plan a roadtrip.  Within seconds, you know how long the trip will take, how many miles it is, and everything in-between (literally).  But what if you don't have a car?  What if you just want to visit a city and don't care how long it takes?  What if you've spent your whole life avoiding danger and now feel like you've some catching up to do?  Enter PITSTOP, the ride-sharing app that combines the best (and worst) parts of Craigslist and Google Maps!  How does it work?  All you need to do is create a new trip from the home page by clicking to indicate your starting point, any stops you want to visit along the way, and your destination.  Create a username for yourself, name your trip, name all the locations, and feel free to include a review for each stop if you've been before.  After creating the trip, other people can see the trip you have planned, and get in contact with you to hitch a ride.  Entrusting your life to strangers is so thrilling! Lastly, if you only want to go to one particular place, you can go to the Stops page to see if your destination is on the list.  If it is, you can reach out to the "owner" of that trip to join them.  

This project marks my first foray into React/Redux, and it was certainly fraught with challenges.  First off, and I hate to make this a point, but this section was almost entirely self-taught for me.  Our cohort lost both of the teachers that we had for all of the previous modules, so we had to rely on teaching ourselves a lot of the lesson content.  Another challenge was simply the sheer scope of the project.  As this was the final project, I felt like I needed to do something exciting and interesting to go out with a bang; however, the amount of work that comes from CSS styling, incorporating a Google Maps API into the app, creating your own Marker components to work with said Google Maps API, creating all of the Actions and Reducers... all of those things took a tremendous amount of time, and there's still more that I want to do.  If I had one piece of advice to give to anyone about to start their React project, it's this: plan ahead.  Make sure you take the time to draft your layouts, the components you'll need, and what you want your state to look like.  Trust me, it takes more time at first, but it will save you so much needless stress later on.

Perhaps the most challenging aspect of my project was getting the Google Maps API to work.  If you haven't implemented Google Maps into your project, here's a crash course:  

1.) npm or yarn install "google-maps-react".

2.) I would suggest your create a "MapContainer" component or something similar to hold your map.  Within that component, you need to import { Map, GoogleApiWrapper, Marker } from 'google-maps-react' if you want those components available.  Keep in mind, there are many more you can import, so check out the Maps API help page for more information!

3.) On the subject of the Google Maps help page, you need to register your Google Account for developer privileges and add certification to your project in order to get an API Key, which you'll need for the map to load properly.  You don't want to give this out, so put it in your .env file in the root directory, and include .env in your .gitignore file as well.  

4.)  The Google API Wrapper needs to actually wrap your container, so you should include it as such (assuming you're using mapStateToProps):

```
export default GoogleApiWrapper({
    apiKey: `${API_KEY}`
})(connect(mapStateToProps, { *Your Dispatch Functions* })(MapContainer));
```

5.) Now all you need to do is render a <Map /> and it should appear! Here are some additional helpful settings you may want to use when you create your <Map /> component:

```
<Map
google={this.props.google}
            style={mapStyles}
            disableDoubleClickZoom
            zoom={6}
            initialCenter={{
                lat: 31.7589382,
                lng: -90.3676974,
            }}
```

The zoom prop tells the map how zoomed-in to your initialCenter target the map should be.  You can tweak these settings as you'd like to have the map load focused on whatever lat and lng coordinates you provide.  Furthermore, you also can include <Marker /> components that will render the default Google Maps marker.  The most important prop for a <Marker /> is its position, which is an object with keys for lat and lng.  If you know where you want your Markers to be all of the time, you can simply map over your Markers array (whether in state or redux store -- in the below example, I use Redux):

```
return this.props.markers.map(
                marker => {
                    return (
                        <Marker 
                        key={marker.id}
                        position={{ lat: marker.position.lat, lng: marker.position.lng }}
                        />
                    )
                }
            )
```

This will create Marker objects at the coordinates specified by your position!  Easy, right? Personally, I would suggest that you store your Markers into your Redux store, and have your MapContainer with a local state set to a marker object.  This way, no matter which component renders your MapContainer, you can easily pull your markers from global state and they'll handle the responsibility of rendering themselves instead of you having to create a function that does so in each new component.

Looking back at my completed project, the Google Maps API was easy to set up, but challenging to get all of the moving parts to work correctly and in conjunction with each other.  That being said, now that everything is up and running, I'm very proud of the completed project and the effort that I put into it.  As a capstone for everything that I've learned thus far, PITSTOP embodies all of my months of hard work.  Next time you want to roll the dice on a random trip to a place you've never been before, maybe you'll consider planning your adventure with PITSTOP!


