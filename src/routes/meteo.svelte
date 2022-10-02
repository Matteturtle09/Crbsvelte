<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>

<script>
    import Navbar from "../components/navbar.svelte";
    import Meteocard from "../components/meteocard.svelte";
    import Footer from "../components/footer.svelte";
</script>
<Navbar></Navbar>
<div class="h-screen w-screen bg-gradient-to-l hover:bg-gradient-to-r from-purple-500 to-pink-500">
<Meteocard></Meteocard>
</div>
<Footer/>