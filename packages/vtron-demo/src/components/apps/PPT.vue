<template>
  <iframe allow="fullscreen" ref="storeRef" src="https://vtron.site/ppt"></iframe>
</template>
<script lang="ts" setup>
import { BrowserWindow, Notify, System } from 'vtron';
import { ref, inject } from 'vue';
const sys = inject<System>('system')!;
const win = inject<BrowserWindow>('browserWindow');
const storeRef = ref<HTMLIFrameElement | null>(null);
let hasInit = false;
window.addEventListener('message', async (e) => {
  const eventData = e.data;
  if (eventData.type == 'exportSpecificFile') {
    await sys.fs.writeFile('/C/Users/Desktop/newPPT.ppt', eventData.data);
    new Notify({
      title: '保存成功',
      content: '文件已保存到桌面',
    });
  } else if (eventData.type == 'initSuccess') {
    if (hasInit) {
      return;
    }
    hasInit = true;
    storeRef.value?.contentWindow?.postMessage(
      {
        type: 'init',
        data: win?.config.content,
      },
      '*'
    );
  }
});
</script>
