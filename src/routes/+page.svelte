<script lang="ts">
    import { FileDropzone } from '@skeletonlabs/skeleton';
    let orientation = "🔽";
    let action = "";
    let file = "";
    let files: FileList | undefined = undefined;
    const clear_form = () => {
        file = "";
        files = undefined;
        if ((document.getElementById("input.email") as HTMLSelectElement) !== null) (document.getElementById("input.email") as HTMLSelectElement).value = "";
        if ((document.getElementById("input.subject") as HTMLSelectElement) !== null) (document.getElementById("input.subject") as HTMLSelectElement).value = "";
        if ((document.getElementById("input.complaint") as HTMLSelectElement) !== null) (document.getElementById("input.complaint") as HTMLSelectElement).value = "";
        if ((document.getElementById("input.other") as HTMLSelectElement) !== null) (document.getElementById("input.other") as HTMLSelectElement).value = "";
    }
    const submit = () => {
        const form = document.getElementById("form.action") as HTMLFormElement;
        if (!form.checkValidity()) return;
        const sel_action = (document.getElementById("select.action") as HTMLSelectElement).value;
        switch (sel_action) {
            case "apply": {
                //do something with file
                reveal();
                break;
            }
            case "complaint": {
                //do something with text
                reveal();
                break;
            }
            case "other": {
                //do something with text
                reveal();
                break;
            }
        }
        action = "";
        clear_form();
        (document.getElementById("select.action") as HTMLSelectElement).value = "";
    }
    const reveal = () => {
        const form = document.getElementById("div.action") as HTMLDivElement;
        if (form.hidden) {
            form.hidden = false;
            orientation = "🔼";
        } else {
            form.hidden = true;
            orientation = "🔽";
        }
    }
    const select = () => {
        const sel_action = (document.getElementById("select.action") as HTMLSelectElement).value;
        clear_form();
        action = sel_action;
    }
    const file_upload = (e: Event) => {
        //get file name
        if (files === undefined) return;
        file = files[0].name;
        if (file.length > 20) {
            file = file.substring(0, 20) + "...";
        }
    }
</script>
<div class="flex flex-col text-center">
    <button class="rounded-md border-t-2 border-l-2 border-black my-2 bg-white font-bold w-[15vw]" on:click={reveal}>{orientation} Contact</button>
    <div class="fixed top-0 left-0 w-screen h-screen bg-black/80" id="div.action" hidden>
        <div class="w-full h-full grid place-content-center">
            <div class="rounded-md border-t-2 border-l-2 border-black py-1 bg-slate-800 w-[15vw] px-1">
                <form class="flex flex-col" id="form.action">
                    <div class="grid place-content-end">
                        <button class="text-right bg-slate-500 border-t-2 border-l-2 border-black rounded-md px-2 hover:bg-orange-300 text-[8px] font-extrabold" on:click={reveal}>X</button>
                    </div>
                    <select class="text-center font-semibold bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1 cursor-pointer" name="Action" id="select.action" on:change={select} required>
                        <option value="" disabled selected>Select Action</option>
                        <option value="apply">Apply</option>
                        <option value="complaint">Complaint</option>
                        <option value="other">Other</option>
                    </select>
                    <input class="text-center bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1" type="email" name="Email" id="input.email" placeholder="Email" required>
                    {#if action === "apply"}
                        <FileDropzone name="files" class="bg-white/5 hover:bg-white/20" accept="application/pdf" bind:files on:change={file_upload}>
                            <svelte:fragment slot="lead">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-[8vw] h-[8vw]">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75V16.5m-13.5-9L12 3m0 0l4.5 4.5M12 3v13.5" />
                                </svg>
                            </svelte:fragment>
                            <svelte:fragment slot="message">Upload</svelte:fragment>
                            <svelte:fragment slot="meta">{file}</svelte:fragment>
                        </FileDropzone>
                    {:else if action === "complaint"}
                        <input class="text-center bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1" type="text" name="Subject" id="input.subject" placeholder="Subject" required>
                        <input class="text-center bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1" type="text" name="Complaint" id="input.complaint" placeholder="Complaint" required>
                    {:else if action === "other"}
                        <input class="text-center bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1" type="text" name="Subject" id="input.subject" placeholder="Subject" required>
                        <input class="text-center bg-slate-600 rounded-md border-t-2 border-l-2 border-black my-1" type="text" name="Other" id="input.other" placeholder="Comment" required>
                    {/if}
                    <input class="text-center font-semibold bg-slate-500 rounded-md border-t-2 border-l-2 border-black hover:bg-blue-400 px-1 my-1 cursor-pointer" type="submit" id="button.submit" on:click={submit} value="Submit">
                </form>
            </div>
        </div>
    </div>
</div>