<script>
  import { onMount } from "svelte";
  import { browser } from "$app/env";
  import { initializeApp } from "firebase/app";
  import { getFirestore, collection, getDocs } from "firebase/firestore";
  //firebase config
  const firebaseConfig = {
    apiKey: "AIzaSyCIsLM4nPnQd-ZE7npIpN7nJ5BBtqCBuXc",
    authDomain: "sito-login-8b85d.firebaseapp.com",
    projectId: "sito-login-8b85d",
    storageBucket: "sito-login-8b85d.appspot.com",
    messagingSenderId: "905951839207",
    appId: "1:905951839207:web:6071c768f8d12add037342",
    measurementId: "G-VHTXVHCWSX",
  };
  //creazione mappa piu markers

  // init firebase
  initializeApp(firebaseConfig);

  // init services
  const db = getFirestore();

  // collection ref
  const colRef = collection(db, "strutture");
  let pois = [];

  onMount(async () => {
    const leaflet = await import("leaflet");
    const map = leaflet.map("map").setView([45.5696792, 10.5406322], 17);
    if (browser) {
      leaflet
        .tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
          attribution:
            '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
        })
        .addTo(map);
      getDocs(colRef)
        .then((snapshot) => {
          // console.log(snapshot.docs)

          snapshot.docs.forEach((doc) => {
            leaflet
            .marker([doc.get("lat"),doc.get("lon")])
            .addTo(map)
            .bindPopup("<h1 class='font-bold text-base'>"+doc.get("name")+"</h1><p class='text-sm'>"+doc.get("desc")+"</p>")
            .openPopup();
           
          });
        })

        .catch((err) => {
          console.log(err.message);
        });
      
          
    }
  });

  function mapclick (){
    document.getElementById('map').focus();
  }
</script>

<main>
  <div on:click={mapclick} id="map" />
</main>

<style>
  @import "https://unpkg.com/leaflet@1.7.1/dist/leaflet.css";
  main #map {
    height:90vh
  }
</style>
