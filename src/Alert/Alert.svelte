<script context="module">
    const styles = ["primary", "success", "warning", "danger"];
    export const alertOptions = {
        styles
    }

    let name = 0;
</script>

<script>
    import uikit from 'uikit';
    import {uk_width} from "..";

    let element, closeElem, options = {}, classes = [];

    export let showClose = false;
    export let largeClose = false;

    export let style = "";
    $: {
        classes = [];
        if (styles.includes(style.toLowerCase())) classes.push("uk-alert-" + style);
        classes = [...classes];
    }

    $: if (element) {
        uikit.alert(element, options);
    }
    $: if (closeElem) {
        uikit.close(closeElem);
    }

    export let width = "";
    let _class = "";
    export {_class as class}

    export let title = "";
</script>
<div use:uk_width={width}>
    <div bind:this={element} class={classes.join(" ") + " " + _class} on:hide on:beforehide>
        {#if showClose}
            <button class="uk-alert-close" bind:this={closeElem} class:uk-close-large={largeClose}></button>
        {/if}
        <h3>
            {title || "Alert!"}
        </h3>
        <slot>
            <p>
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Adipisci aliquid cupiditate dignissimos,
                dolores
                eius,
                enim eos expedita in libero molestiae nisi odit quae, quas quis ratione recusandae reiciendis sed
                ullam.
            </p>
        </slot>
    </div>
</div>