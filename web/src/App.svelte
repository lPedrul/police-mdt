<script lang="ts">
  import { CONFIG, IS_BROWSER } from './stores/stores';
  import { InitialiseListen } from '@utils/listeners';
  import Visibility from '@providers/Visibility.svelte';
  import TabletOverlay from '@components/TabletOverlay.svelte';
  import Dashboard from '@components/Dashboard.svelte';
  import { sineIn } from 'svelte/easing';
  import {
    Drawer,
    Button,
    CloseButton,
    Sidebar,
    SidebarBrand,
    SidebarCta,
    SidebarDropdownItem,
    SidebarDropdownWrapper,
    SidebarGroup,
    SidebarItem,
    SidebarWrapper,
    Tooltip,
    Tabs,
    TabItem,
  } from 'flowbite-svelte';
  import {
    ChartPieSolid,
    CartSolid,
    GridSolid,
    MailBoxSolid,
    UsersSolid,
    ShoppingBagSolid,
    ArrowRightToBracketOutline,
    EditOutline,
    BarsOutline,
    UserSolid,
    CloseOutline,
    FolderOpenSolid,
    TruckSolid,
    ExclamationCircleSolid,
  } from 'flowbite-svelte-icons';

  const sidebarItems = [
    {
      itemId: 'dashboard',
      itemName: 'Dashboard',
      icon: ChartPieSolid,
      itemContent: Dashboard,
    },
    {
      itemId: 'profiles',
      itemName: 'Profile',
      icon: UserSolid,
    },
    {
      itemId: 'incidents',
      itemName: 'Incidents',
      icon: FolderOpenSolid,
    },
    {
      itemId: 'reports',
      itemName: 'Reports',
      icon: FolderOpenSolid,
    },
    {
      itemId: 'warrants',
      itemName: 'BOLOs/Warrants',
      icon: ExclamationCircleSolid,
    },
    {
      itemId: 'vehicles',
      itemName: 'Vehicles',
      icon: TruckSolid,
    },
  ];

  let openTabs: {
    tabName: string;
    tabContent: __sveltets_2_IsomorphicComponent<any>;
  }[] = $state([]);

  openTab({
    tabName: 'Test',
    tabContent: Dashboard,
  });

  function openTab(tabInfo: {
    tabName: string;
    tabContent: __sveltets_2_IsomorphicComponent<any>;
  }) {
    openTabs.push(tabInfo);
    openTabs = openTabs;
  }

  function closeTab(tabInfo: {
    tabName: string;
    tabContent: __sveltets_2_IsomorphicComponent<any>;
  }) {
    const index = openTabs.indexOf(tabInfo);
    if (index > -1) openTabs.pop();
  }

  CONFIG.set({
    fallbackResourceName: 'debug',
    allowEscapeKey: true,
  });

  InitialiseListen();
</script>

<Visibility>
  <TabletOverlay>
    <div class="bg-gray-800 flex flex-row h-full w-full">
      <!-- Sidebar -->
      <div class="bg-gray-700 px-1 py-2">
        <Sidebar class="relative top-[30%]">
          <SidebarWrapper>
            <SidebarGroup class="flex flex-col">
              {#each sidebarItems as sidebarItem}
                <SidebarItem
                  href="#"
                  id={`sdb-${sidebarItem.itemId}`}
                  on:click={() =>
                    openTab({
                      tabName: sidebarItem.itemName,
                      tabContent: sidebarItem.itemContent as any,
                    })}
                >
                  <svelte:fragment slot="icon">
                    <sidebarItem.icon
                      class="my-2 h-[30px] w-[30px] text-gray-500 transition duration-75"
                    />
                  </svelte:fragment>
                </SidebarItem>
                <Tooltip
                  class="rounded-md bg-gray-600 px-3 py-1"
                  triggeredBy={`#sdb-${sidebarItem.itemId}`}
                  placement="right"
                >
                  {sidebarItem.itemName}
                </Tooltip>
              {/each}
            </SidebarGroup>
          </SidebarWrapper>
        </Sidebar>
      </div>

      <!-- Main Container -->
      <div class="mx-2 my-2 justify-self-center w-full flex flex-col">
        <div
          class={`shrink h-full w-full mb-10 ${openTabs.length === 0 ? 'invisible' : ''}`}
        >
          <Tabs contentClass="h-full w-full bg-gray-700 rounded-br-xl">
            {#each openTabs as openTab}
              <TabItem
                open
                title={openTab.tabName}
                class="bg-gray-700 px-3 py-1 mb-2 text-md font-bold mr-2"
              >
                <Button
                  on:click={() => closeTab(openTab)}
                  class="absolute right-4 bg-red-500 rounded-md px-1 mt-2"
                  ><CloseOutline /></Button
                >
                <openTab.tabContent />
              </TabItem>
            {/each}
          </Tabs>
        </div>
      </div>
      <!-- Sub Containers -->
    </div>
  </TabletOverlay>
</Visibility>

{#if import.meta.env.DEV}
  {#if $IS_BROWSER}
    {#await import('./providers/Debug.svelte') then { default: Debug }}
      <Debug />
    {/await}
  {/if}
{/if}
