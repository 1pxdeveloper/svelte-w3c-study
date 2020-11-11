<script>
import {Router, Route} from "svelte-routing"
import Home from "./pages/Home.svelte"
import MemoryGame from "./pages/study/MemoryGame.svelte"
</script>

<Router>
  <Route path="/" component="{Home}"/>
  <Route path="/study/memory-game" component="{MemoryGame}"/>
</Router>