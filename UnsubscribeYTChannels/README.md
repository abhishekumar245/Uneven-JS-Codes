# UnsubscribeYTChannels
A small code to unsubscribe YouTube channels.

# How To?
1. Open Chrome.
2. Then open YouTube.
3. Open `Developer Tools` by shortcut `CTRL + SHIFT + I`.
4. Open Console Tab.
5. Clear by shortcut `CTRL + L`.
6. Copy and Paste the code below in it :
```
const controller = new AbortController();
const signal = controller.signal;

(async function iife() {
    try {
        var UNSUBSCRIBE_DELAY_TIME = 2000;
        var runAfterDelay = (fn, delay) => new Promise((resolve) => {
            setTimeout(() => {
                if (!signal.aborted) fn();
                resolve();
            }, delay);
        });

        var channels = Array.from(document.getElementsByTagName(`ytd-channel-renderer`));
        console.log(`${channels.length} channels found.`);
        var ctr = 0;

        for (const channel of channels) {
            if (signal.aborted) break;
            const unsubscribeButton = channel.querySelector(`[aria-label^='Unsubscribe from']`);
            if (unsubscribeButton) {
                unsubscribeButton.click();
                await runAfterDelay(() => {
                    const dialogContainer = document.getElementsByTagName(`yt-confirm-dialog-renderer`)[0];
                    if (dialogContainer) {
                        const confirmButton = dialogContainer.querySelector(`[aria-label^='Unsubscribe']`);
                        if (confirmButton) {
                            confirmButton.click();
                            ctr++;
                            console.log(`Unsubscribed ${ctr}/${channels.length}`);
                        }
                    }
                }, UNSUBSCRIBE_DELAY_TIME);
            }
        }
    } catch (e) {
        if (signal.aborted) {
            console.log("Script aborted.");
        }
    }
})();
```
7. Press Enter.
8. Wait for sometime, all channels will be unsusbcribed one by one.