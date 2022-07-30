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
  var pnome;
  var pdesc;
  var plat;
  var plon;

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
    });
  }

  async function modifystr(id, nome, desc, imgpath ) {
    await setDoc(doc(db, "strutture", id), {
      name: nome,
      desc: desc,
      imgpath: imgpath,
    });
  }

   async function modifypoi(id, nome, desc, lat, lon ) {
    await setDoc(doc(db, "pois", id), {
      name: nome,
      desc: desc,
      lat: lat,
      lon: lon,
    });
  }

  function addpoi() {
    const docRef = addDoc(collection(db, "pois"), {
      name: pnome,
      desc: pdesc,
      lat: plat,
      lat: plon,
    });
  }

  // referenza collezione
  const colRefstr = collection(db, "strutture");
  const colRefpois = collection(db, "pois");
  onMount(async () => {
    if (browser) {
      getDocs(colRefstr).then((snapshot) => {
        snapshot.docs.forEach((doc) => {
          strutture.push({ ...doc.data(), id: doc.id });
          strutture = strutture;
        });
        console.log(strutture);
      });

      getDocs(colRefpois).then((snapshot) => {
        snapshot.docs.forEach((doc) => {
          pois.push({ ...doc.data(), id: doc.id });
          pois = pois;
        });
        console.log(pois);
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
        <th>Id</th>
      </tr>
    </thead>
    <tbody>
      {#each strutture as str}
        <tr>
          <th />
          <th
            ><input
              on:click={modifystr(str.id,str.name,str.desc,str.imgpath)}
              bind:value={str.name}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></th
          >
          <td
            ><input
              on:click={modifystr(str.id,str.name,str.desc,str.imgpath)}
              bind:value={str.desc}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td
          >
          <td
            ><input
              on:click={modifystr(str.id,str.name,str.desc,str.imgpath)}
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
          ><button class="btn btn-outline btn-success" on:click={add}
            >ADD</button
          ></td
        >
      </tr>
    </tbody>
  </table>
</div>

<div class="overflow-x-auto my-8">
  <table class="table table-zebra w-full">
    <!-- head -->
    <thead>
      <tr>
        <th />
        <th>Name</th>
        <th>Desc</th>
        <th>lat</th>
        <th>lon</th>
        <th>Id</th>
      </tr>
    </thead>
    <tbody>
      {#each pois as poi}
        <tr>
          <th />
          <th><input
              on:click={modifypoi(poi.id,poi.name,poi.desc,poi.lat,poi.lon)}
              bind:value={poi.name}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></th>
          <td><input
              on:click={modifystr(poi.id,poi.name,poi.desc,poi.lat,poi.lon)}
              bind:value={poi.desc}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td>
          <td><input
              on:click={modifystr(poi.id,poi.name,poi.desc,poi.lat,poi.lon)}
              bind:value={poi.lat}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td>
          <td><input
              on:click={modifystr(poi.id,poi.name,poi.desc,poi.lat,poi.lon)}
              bind:value={poi.lon}
              type="text"
              placeholder="Type here"
              class="input input-ghost w-full max-w-xs"
            /></td>

          <td>{poi.id}</td>
        </tr>
      {/each}
      <tr>
        <th />
        <td
          ><input
            type="text"
            bind:value={pnome}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={pdesc}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={plat}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><input
            type="text"
            bind:value={plon}
            placeholder="Type here"
            class="input input-bordered input-success w-full max-w-xs"
          /></td
        >
        <td
          ><button class="btn btn-outline btn-success" on:click={addpoi}
            >ADD</button
          ></td
        >
      </tr>
    </tbody>
  </table>
</div>
