<script>
import {Link} from "svelte-routing"
export let href = ""
</script>

<Link to={href}><slot/></Link>