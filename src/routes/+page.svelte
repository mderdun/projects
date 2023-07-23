<script>
	import Tab1 from "./tabs/Tab1.svelte";
    import Tab2 from "./tabs/Tab2.svelte";
    import Tab3 from "./tabs/Tab3.svelte";
  import Tabs from "./tabs/tabs.svelte";

  // List of tab items with labels, values and assigned components
  let items = [
    { label: "1",
		 value: 1,
		 component: Tab1,
         bgcolor: "#74c0fc"
		},
    { label: "2",
		 value: 2,
		 component: Tab2,
         bgcolor: "#e03131"
		},
    { label: "3",
		 value: 3,
		 component: Tab3,
         bgcolor: "#40c057"
		}
  ];
</script>

<Tabs {items} />