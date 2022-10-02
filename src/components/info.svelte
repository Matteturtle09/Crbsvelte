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

  // inizializza firebase
  initializeApp(firebaseConfig);

  // strutture array
  let strutture = [

  ];

  // init services
  const db = getFirestore();

  // referenza collezione
  const colRef = collection(db, "strutture");
onMount(async () => {
  if(browser){
  getDocs(colRef)
    .then((snapshot) => {
      
     snapshot.docs.forEach((doc) => {
       strutture.push({ ...doc.data(), id: doc.id });
       strutture = strutture;
      });
      console.log(strutture);
      })
  }
 });

</script>

{#each strutture as str}
<div class="flex flex-col space-y-8  mx-2">
  <div class="card w-xl bg-base-100 shadow-xl self-center ">
    <figure ><img src={str.imgpath} alt={str.name} /></figure>
    <div class="card-body ">
      <h2 class="card-title">{str.name}</h2>
      <p>{str.desc}</p>
      <div class="card-actions justify-end" />
    </div>
  </div>
</div>
{/each}

