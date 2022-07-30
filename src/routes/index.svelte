<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>
<script>
    import Navbar from "../components/navbar.svelte";
    import Hero from "../components/hero.svelte";
    import Info from "../components/info.svelte";
    import Footer from "../components/footer.svelte";

</script>
<Navbar></Navbar>
<div class="flex flex-col space-y-8 ">
<Hero></Hero>

<Info/>

<Footer/>
</div>