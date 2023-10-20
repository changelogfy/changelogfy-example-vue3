<script setup>
import { onMounted, ref } from "vue";

const total = ref(0);

const loadScript = async () => {
  const script = document.createElement("script");
  script.setAttribute("src", "https://widget.changelogfy.com/index.js");
  script.async = true;
  document.head.appendChild(script);
};

const startChangelogfy = async () => {
  window.CLF_config = {
    app_id: "YOUR_APP_ID",
    selector: ".changelogfy-widget",
    data: {
      user_email: "",
      user_id: "",
      user_name: "",
    },

    callbacks: {
      onReady: function () {
        console.log("widget ready");
        console.log(`unread entries count: ${changelogfy.getUnreadCount()}`);

        total.value = changelogfy.getUnreadCount();
      },

      onOpen: function () {
        console.log("widget opened");
      },
      onClose: function () {
        console.log("widget closed");
      },
    },
  };
};

onMounted(async () => {
  await loadScript();
  await startChangelogfy();
});
</script>

<template>
  <div class="card">
    <button type="button" class="changelogfy-widget">Open Changelogfy</button>
  </div>

  <div class="card">
    <div>
      <div>Total Notifications</div>
      <div>{{ total }}</div>
    </div>
  </div>
</template>
