<script>
  import { onMount } from "svelte";
  import { browser } from "$app/env";
  import { initializeApp } from "firebase/app";
  import {
    getFirestore,
    collection,
    getDocs,
    addDoc,
    doc,
    deleteDoc,
    setDoc,
  } from "firebase/firestore";

  var nome;
  var desc;
  var imgpath;
  var lat;
  var lon;

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
  let strutture = [];
  let pois = [];

  // init services
  const db = getFirestore();

  function add() {
    const docRef = addDoc(collection(db, "strutture"), {
      name: nome,
      desc: desc,
      imgpath: imgpath,
      lat: lat,
      lon: lon,
    });
  }

  async function modifystr(id, nome, desc, imgpath) {
    await setDoc(doc(db, "strutture", id), {
      name: nome,
      desc: desc,
      imgpath: imgpath,
      lat: lat,
      lon: lon,
    });
  }

  // referenza collezione
  const colRefstr = collection(db, "strutture");
  onMount(async () => {
    if (browser) {
      getDocs(colRefstr).then((snapshot) => {
        snapshot.docs.forEach((doc) => {
          strutture.push({ ...doc.data(), id: doc.id });
          strutture = strutture;
        });
        console.log(strutture);
      });
    }
  });
</script>

<div class="overflow-x-auto my-8">
  <table class="table table-zebra w-full">
    <!-- head -->
    <thead>
      <tr>
        <th />
        <th>Name</th>
        <th>Desc</th>
        <th>Imgpath</th>
        <th>Latitudine</th>
        <th>Longitudine</th>
        <th>Id</th>
      </tr>
    </thead>
    <tbody>
      {#each strutture as str}
        <tr>
          <th />
          <th
            ><input
              on:click={modifystr(str.id, str.name, str.desc, str.imgpath)}
              bind:value={str.name}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></th
          >
          <td
            ><input
              on:click={modifystr(str.id, str.name, str.desc, str.imgpath)}
              bind:value={str.desc}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td
          >
          <td
            ><input
              on:click={modifystr(str.id, str.name, str.desc, str.imgpath)}
              bind:value={str.imgpath}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td
          >

          <td
            ><input
              on:click={modifystr(str.id, str.name, str.desc, str.imgpath)}
              bind:value={str.imgpath}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td
          >

          <td
            ><input
              on:click={modifystr(str.id, str.name, str.desc, str.imgpath)}
              bind:value={str.imgpath}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td
          >
          <td>{str.id}</td>
        </tr>
      {/each}
      <tr>
        <th />
        <td
          ><input
            type="text"
            bind:value={nome}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={desc}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={imgpath}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={lat}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
        ><input
          type="text"
          bind:value={lon}
          placeholder="Type here"
          class="input input-bordered input-success w-full max-w-xs"
        /></td
      >
        <td
          ><button class="btn btn-outline btn-success" on:click={add}
            >ADD</button
          ></td
        >
      </tr>
    </tbody>
  </table>
</div>
