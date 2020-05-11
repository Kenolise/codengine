---
title: PWA? Who cares?
date: '2020-05-10'
spoiler: How to transform your React App to a Progressive Web App.
---

What is a Progressive Web Application (PWA)?

A Progressive Web App (PWA) is a web app that uses modern web capabilities to deliver an app-like experience to users.
It delivers a new level of quality, which allows Progressive Web Apps to earn a place on the user's home screen.

Who cares?

Your user does!

Nowadays the expectation from our websites is very high. Over two decades ago when the website was invented, its sole purpose was to share information.
Today, the website can do almost anything. Today, more than 60% of total internet usage is happening via mobile phone.
Wanna know how many mobile devices there are today?

[5.16 billion according to to the latest data from GSMA Intelligence](https://datareportal.com/global-digital-overview) Yeah, that many.

It is important to have fast loading web apps, to improve experience of your users. Statiscally speaking, if your web page load time goes form 1 second to 10 seconds, there is a 123% probability the user will leave the web page. Of course, do you think your users are going to want to wait 10 seconds for your web page to load?
Beyond speed, interaction also matter, splash screen, your users should never be left wondering whether their interaction was registered or not, for example, user clicking a button and there is not change is color or any form of animation on the button, user is unsure if the action was registered.

Finally, reliable applications need to be usable regardless of network connection. Users expect apps to start up on slow or flaky network connections or even when offline. When a request isn't possible due to poor connection or any event, users expect to be told there's trouble instead of the site failing or crashing.

Installed Progressive Web Apps run in a standalone window instead of a browser tab. They're launchable from on the user's home screen, dock, taskbar, or shelf. It's possible to search for them on a device and jump between them with the app switcher, making them feel like part of the device they're installed on. Similar to native applications.

You see these three things mentioned above are the pillars of Progressive Web Applications. They are web applications that have been designed so they are capable, reliable, and installable. 

Only with modern UI frameworks?
No no no, Few people think that a PWA is coupled with the latest UI frameworks like ReactJs, Angular 6 or Vue.js. Well, not necessarily. PWA has nothing to do with the framework you are using, it only needs the required components.
Shortly we'll look at what the components structure of a PWA should look like.

1. Register a Service Worker
What is a service worker?
Service workers (client-side proxies that pre-cache key resources) enable PWAs to load instantly and provide an instant,
reliable experience for users, regardless of the network state.

Create a new worker.js file in the public folder (public/worker.js) and add the following code:
Let CACHE_NAME = 'your-app-name';
Let urlsToCache = [
  '/',
  '/completed'
];

// Install a service worker
self.addEventListener('install', event => {
  // Perform install steps
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(function(cache) {
        console.log('Opened cache');
        return cache.addAll(urlsToCache);
      })
  );
});

// Cache and return requests
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(function(response) {
        // Cache hit - return response
        if (response) {
          return response;
        }
        return fetch(event.request);
      }
    )
  );
});

// Update a service worker
self.addEventListener('activate', event => {
  Let cacheWhitelist = ['your-app-name'];
  event.waitUntil(
    caches.keys().then(cacheNames => {
      return Promise.all(
        cacheNames.map(cacheName => {
          if (cacheWhitelist.indexOf(cacheName) === -1) {
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
});
Note! from above code replace (your-app-name) with your app name

2. Now Update HTML
Update your index.html file in the public folder (public/index.html)
to check if the client’s browser supports service workers. Just Add below code inside the body tag of your app's (public/index.html)
<script>
      if ('serviceWorker' in navigator) {
        window.addEventListener('load', function() {
          navigator.serviceWorker.register('worker.js').then(function(registration) {
            console.log('Worker registration successful', registration.scope);
          }, function(err) {
            console.log('Worker registration failed', err);
          }).catch(function(err) {
            console.log(err);
          });
        });
      } else {
        console.log('Service Worker is not supported by browser.');
      }
    </script>
3. Activating ServiceWorker
Now go to your app's index.js in the src folder (src/index.js)

Now Update serviceWorker.unregister() to serviceWorker.register() Like Below Code At Last Line
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.register();
Restart (npm start) and reload your React app — you should see the message “Worker registration successful” in the console.

4. Create a manifest.json file
Manifest is a simple JSON file that tells the browser about your web application and how it should behave when 'installed' on the user's mobile device or desktop. Having a manifest is required by Chrome to show the Add to Home Screen prompt.

A typical manifest file includes information about the app name, icons it should use, the start_url it should start at when launched, and more.
{
    "name": "your-app-name",
    "short_name": "your-app-name",
    "icons": [
        {
            "src": "img/logo.png",
            "sizes": "92x92",
            "type": "image/png"
        },
        {
            "src": "/img/logo.png",
            "sizes": "144x144",
            "type": "image/png"
        },
        {
            "src": "img/logo.png",
            "sizes": "152x152",
            "type": "image/png"
        }        
    ],
    "start_url": "/",
    "display": "standalone",
    "orientation": "portrait",
    "background_color": "#f0f2f5",
    "theme_color": "#96f2d7"
}


That's it 🎉 Congratulations, you just created a working progressive web app!
Give A heart ❤️ To Appreciate My Work And Follow Me For More Awesome Content.
This Is "irshad ali"
Check Out React PWA Demo: https://www.irshadali.site