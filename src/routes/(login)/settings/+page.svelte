<script lang="ts">
  import Helper from "$lib/components/ui/Helper.svelte";
  import { getSettings } from "$lib/scripts/req";
  import { t, locale, locales } from "$lib/scripts/i18n";
  import { onMount } from "svelte";
  import { apiurl } from "$lib/scripts/req";
  import { pburl } from "$lib/scripts/req";

  function readSettings() {
    getSettings().then((res) => {
      console.log("response:" + res.enablePay);
      //set element "webport"'s placeholder to res.webport
      //set checkbox "enablepay" to res.enablePay
      if (res.enablePay == true) {
        //add checkked attribute to checkbox
        //document.getElementById("enablepay").setAttribute("checked", "");
      }
      document.getElementById("serversperuser").placeholder =
        res.serversPerUser;
      document.getElementById("weblogo").placeholder = res.webLogo;
      document.getElementById("trusteddomains").placeholder =
        res.trustedDomains;
    });
    document.getElementById("browsertitle").placeholder = res.browserTitle;
  }
  onMount(() => {
    readSettings();
  });
</script>

<div class="flex justify-center">
  <div class="flex flex-col max-w-2xl">
    <div class="divider px-10 text-3xl font-semibold">
      {$t("settings.title")}
    </div>
    <p class="text-center mt-2">
      {$t("settings.desc")}
    </p>
    <div class="divider text-xl font-semibold mt-8">
      {$t("settings.h.general")}
    </div>
    <form id="settingsForm">
      <p class="label">Quartz URL</p>
      <div class="flex space-x-2">
        <input
          id="webport"
          class="input-bordered input-primary input w-full max-w-xs bg-base-300"
          type="text"
          placeholder={apiurl}
        />
      </div>
      <p class="label">Pocketbase URL</p>
      <div class="flex space-x-2">
        <input
          id="webport"
          class="input-bordered input-primary input w-full max-w-xs bg-base-300"
          type="text"
          placeholder={pburl}
        />
      </div>
      <p class="label">Maximum # of servers each user can create</p>
      <div class="flex space-x-2">
        <input
          id="serversperuser"
          class="input-bordered input-primary input w-full max-w-xs bg-base-300"
          type="text"
          placeholder=""
        />
      </div>

      <p class="label">Panel Logo</p>
      <div class="flex space-x-2">
        <input
          id="weblogo"
          class="input-bordered input-primary input w-full max-w-xs bg-base-300"
          type="text"
          placeholder=""
        />
        <img
          src="/images/sitelogo.svg"
          width="60ch"
          height="60ch"
          alt="The current Panel logo."
        />
      </div>

      <div class="cursor-pointer label">
        <p class="label-text">Payment Features</p>
        <input id="enablepay" type="checkbox" class="toggle toggle-primary" />
      </div>

      <div class="divider text-xl font-semibold mt-8 mb-6">
        {$t("settings.h.trusted")}
      </div>

      <p>
        {$t("settings.desc.trusted")}
      </p>
      <input
        id="trusteddomains"
        class="input-bordered input-primary input w-full max-w-xs bg-base-300 my-4"
        type="text"
        placeholder=""
      />

      <div>
        <input type="submit" value={$t("button.save")} class="btn btn-block" />
      </div>
    </form>
  </div>
</div>
