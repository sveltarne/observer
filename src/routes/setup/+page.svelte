<script>
  let steps = 0;
  import APISettings from "$lib/components/ui/ApiSettings.svelte";
  import Navbar from "$lib/components/layout/Navbar.svelte";
  import { apiurl } from "$lib/scripts/req";
  import Settings from "$lib/components/ui/Settings.svelte";
  import { fade } from "svelte/transition";

  function step() {
    steps++;
    var step2 = steps + "";
    //add the class "step-secondary" to the element with the id of steps
    document.getElementById(step2).classList.add("step-secondary");
    if (steps == 1) {
      //add property disabled to id "ckbx"
      document.getElementById("ckbx").disabled = true;

      document.getElementById("step2").classList.remove("hidden");
    }
    if (steps == 2) {
      //add class disabled to id "dld"
      document.getElementById("dld").classList.add("btn-disabled");
      document.getElementById("step3").classList.remove("hidden");
      document.getElementById("finish").classList.remove("invisible");
    }
  }
</script>

<Navbar navType="welcome" />
<div class="p-7" />
<div class="grid  items-center">
  <ul class="steps">
    <li id="0" class="step step-secondary">Set Backend URLs</li>
    <li id="1" class="step">Download your key</li>
    <li id="2" class="step">Adjust Settings</li>
    <li id="3" class="step">Complete</li>
  </ul>
  <div class="flex flex-col items-center">
    <div class="divider text-xl p-3">Backend URLs</div>
    <p class="p-3">
      To change these, add QUARTZ_URL and PB_URL environment variables.
    </p>
    <APISettings />
    <input
      type="checkbox"
      id="ckbx"
      class="checkbox checkbox-success m-5"
      on:click={step}
    />
  </div>
  <div class="flex flex-col items-center hidden" id="step2">
    <div class="divider text-xl">Download your key</div>
    <p class="p-3">
      To access some admin-only parts of this panel like settings, you need a
      private key. Keep it safe, you can <b>only download it once.</b>
    </p>
    <a target="_blank" href="{apiurl}panel-key" download
      ><button id="dld" class="btn btn-secondary" on:click={step}
        >Download Key</button
      ></a
    >
  </div>

  <div class="flex flex-col pl-10 hidden" id="step3">
    <div class="divider text-xl p-3">Settings</div>
    <Settings />
  </div>
  <button class="btn btn-block invisible" id="finish" on:click={step}
    ><a href="/">Finish Setup</a></button
  >
</div>
