<script context="module">
    const colors = ["default", "primary", "secondary"];
    const sizes = ["small", "large"];
    export const cardOptions = {
        colors,
        sizes
    }
</script>

<script>
    import {Badge, uk_width} from "..";

    export let title = "";
    export let titleIsHeader = false;

    let classes = ["uk-card", "uk-card-body"];

    export let color = "";
    $: {
        classes = ["uk-card", "uk-card-body"];
        if (colors.includes(color.toLowerCase())) classes.push("uk-card-" + color);
        else classes.push("uk-card-default");
        if (sizes.includes(size.toLowerCase())) classes.push("uk-card-" + size);
        if (hover) classes.push("uk-card-hover");
        classes = [...classes];
    }

    export let size = "";


    export let hover = false;

    export let badge = false;

    export let width = "";


    let headerElement = false;
    let footerElement = false;

    let _class = "";
    export {_class as class}
</script>


<div class={classes.join(" ") + " " + _class} use:uk_width={width}>
    <div class:uk-card-header={!headerElement} class:uk-hidden={headerElement}
         class="uk-margin-small-bottom uk-padding-remove-horizontal">
        <slot name="header">
            <div bind:this={headerElement}></div>
        </slot>
    </div>

    <div class:uk-hidden={!headerElement} class:uk-card-header={titleIsHeader}>
        <h3 class="uk-card-title uk-margin-remove">{title}</h3>
    </div>

    <div class="uk-margin-small-top">
        <slot/>
    </div>

    {#if badge}
        <Badge card={true} text={badge}/>
    {/if}

    <div class:uk-card-footer={!footerElement}>
        <slot name="footer">
            <div bind:this={footerElement}></div>
        </slot>
    </div>
</div>
