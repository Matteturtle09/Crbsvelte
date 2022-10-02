<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>

<script>
    import Navbar from "../components/navbar.svelte";
    import Tabella from "../components/tabella.svelte";
    import { initializeApp } from 'firebase/app';
    import Footer from "../components/footer.svelte";
    import { getAuth, signInWithEmailAndPassword, browserSessionPersistence, setPersistence } from "firebase/auth";
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
  // email and password variables
  let email;
  let password;
  var user;
  // init services
 

  const auth = getAuth();
  function signin(){
   
   signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in 
    setPersistence(auth, browserSessionPersistence)
    user = userCredential.user;
    
    // ...
  })
  .catch((error) => {
    console.log(error);
  });
  }

</script>
<Navbar></Navbar>
<!-- svelte-ignore empty-block -->
<!-- svelte-ignore missing-declaration -->
{#if user}
  <Tabella/>
{:else}
<div class="form-control my-8 space-y-4 mx-2 self-center items-center ">
  
  <p class="text-3xl text-green-500 text-bold">LOG IN</p>
  <input type="email" placeholder="email" bind:value={email} class="input focus:input-success w-full max-w-xs" />
  <input type="Password" placeholder="password" bind:value={password} class="input focus:input-success w-full max-w-xs" />
  <button class="btn btn-outline btn-success " on:click={signin}>Log in</button>
</div>
{/if}
<Footer/>