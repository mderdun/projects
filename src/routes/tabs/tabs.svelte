<!-- TabComponent.svelte -->
<script>
    import '../../app.css'
    export let items = [];
    export let activeTabValue = 1;
  
    const handleClick = (tabValue) => {
      activeTabValue = tabValue;
  
      // Get the selected tab's color
      const selectedTab = items.find(item => item.value === tabValue);
      const selectedColor = selectedTab ? selectedTab.bgcolor : '';
  
      // Set the background color of the content area to the selected color
      document.querySelector('.content').style.backgroundColor = selectedColor;
  
      // Set the border color of the content area to the selected tab's border color
      document.querySelector('.content').style.borderColor = selectedTab ? selectedTab.bordercolor : '';
    };
  
    const handleKeyDown = (event) => {
      if (event.key === 'Enter') {
        const tabValue = Number(event.currentTarget.dataset.tabValue);
        handleClick(tabValue);
      }
    };
  </script>
  
  <div class="container">
    <ul class="tab-bar">
      {#each items as item}
        <li class={activeTabValue === item.value ? "active" : ""}>
          <span
            class="tab-button"
            style={`background-color: ${item.bgcolor}; ${
              activeTabValue === item.value ? "color: white;" : ""
            }`}
            on:click={() => handleClick(item.value)}
            role="button"
            tabindex="0"
            data-tab-value={item.value}
            on:keydown={handleKeyDown}
          >
            {item.label}
          </span>
        </li>
      {/each}
    </ul>
    <div class="content">
      {#each items as item}
        {#if activeTabValue === item.value}
          <div class="box">
            <svelte:component this={item.component} />
          </div>
        {/if}
      {/each}
    </div>
  </div>
  
  <style>
    /* Base styles */
    .container {
      display: flex;
      height: 100vh; /* Adjust the height as needed */
      border: none;
    }
  
    .tab-bar {
      display: flex;
      background-color: '#ffe8cc';
      flex-direction: column;
      flex-wrap: wrap;
      padding-left: 0;
      margin-bottom: 0;
      list-style: none;
      border-right: none;
      justify-content: flex-start; /* Adjust the alignment as needed */
      align-items: center; /* Adjust the alignment as needed */
      z-index: 2;
    }
  
    li {
      margin-bottom: -1px;
    }
  
    .tab-button {
      font-family: var(--robo);
      font-size: 4rem;
      text-align: center;
      margin-bottom: 0.5rem;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 25vh;
      box-sizing: border-box;
      aspect-ratio: 1 / 1;
      max-width: 115px;
      border: 1px solid transparent;
      border-top-left-radius: 0.5rem;
      border-bottom-left-radius: 0.5rem;
      border-top-right-radius: 0rem;
      display: block;
      padding: 0.5rem 1rem;
      cursor: pointer;
      transition: 0.3s ease; /* Animation on background-color change */
      color: var(--button-color);
      background-color: var(--button-bg-color);
      z-index: 3;
    }
  
    .tab-button:hover {
      border-color: yellow;
      border-style: dashed;
      border-right: none;
      border-width: 0.2rem;
      opacity: 1;
    }
  
    li.active > .tab-button {
      color: white;
      background-color: #fff;
      border: none;
      border-right: none;
      opacity: 1;
      box-shadow: 0 3px 0.1rem gray;
    }
  
    li:not(.active) > .tab-button {
      opacity: 0.5;
      box-shadow: 0 5px 0.3rem gray;
    }
  
    li:not(.active) > .tab-button:hover {
      opacity: 0.8;
      color: #fff;
      background-color: var(--button-color);
      box-shadow: 0 3px 0.25rem gray;
    }
  
    /* Define CSS variables for the tab buttons */
    .tab-bar {
      --button-color: black;
      --button-bg-color: white;
    }
  
    /* Define CSS variable for the content border color */
    .content {
      flex: 1;
      overflow-y: auto; /* Add a scrollbar when content overflows */
      padding: 0; /* Remove padding to close the gap between tab and content */
      display: flex;
      flex-direction: column;
      justify-content: stretch; /* Adjust the alignment to stretch content vertically */
      align-items: stretch; /* Adjust the alignment to stretch content horizontally */
      border-left: none;
      border-radius: 10px;
      border: black 0.3rem solid; /* Add the content border */
      z-index: 1;
    }
  
    .box {
      margin: 0; /* Remove margin to close the gap between tab and content */
      padding: 40px;
      border: 1px solid #dee2e6;
      border-radius: 0 0 0.5rem 0.5rem;
      border-top: 0;
      border-left: 0;
      flex: 1; /* Allow the box to stretch and fill available space */
      z-index: 1;
    }
  </style>
  