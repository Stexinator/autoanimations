<script>
    import { getContext }   from "svelte";

    //export let animation;
    //export let category;
    //export let idx;
    export let section;
    export let section02;

    let { animation, category, idx } = getContext('animation-data');

    $: isCustom = $animation[section][section02].enableCustom;

    const label = game.i18n.localize('autoanimations.menus.custom')
    function removeMetaData() {
       delete $animation.metaData
   }
</script>

<table class="c">
    <tr>
        <td style="border: none;">
            <div class="flexrow">
                <label for="" class="aa-customFont">{label}</label>
                <input
                type="checkbox"
                id="{section} {section02} {animation._data.id}"
                bind:checked={$animation[section][section02].enableCustom}
                on:change={() => removeMetaData()}
                />
            </div>
        </td>
        <td style=" border: none" class={isCustom ? "" : "aa-disableOpacity"}>
            <input
            disabled={!isCustom}
            type="text"
            bind:value={$animation[section][section02].customPath}
            on:change={() => removeMetaData()}
            style="font-weight:normal; font-size:small; border-radius: 5px;text-align:left; width: 100%;"
            />
        </td>
        <td style="border: none" class={isCustom ? "" : "aa-disableOpacity"}>
            <i class="fas fa-file-import"
               title="File Picker"
               style="font-size:1.5em"
               on:click|preventDefault={() => category.selectCustom(section, section02, idx)}
               role=presentation
            />
            <i class="fas fa-database"
               title="Sequencer Database Viewer"
               style="font-size:1.5em;margin-left: 5px"
               on:click|preventDefault={() => category.openSequencerViewer()}
               role=presentation
            />
        </td>
    </tr>
</table>

<style lang="scss">
    table.c label {
        margin-top: .2em;
    }
    .aa-customFont {
        font-family: "Modesto Condensed", "Palatino Linotype", serif;
        font-weight: bold;
        font-size: 1.5em;
    }
    input[type=checkbox]{
        max-width: 1.5em;
    }
    input[type=checkbox]:checked::after{
        content: "";
    }
        input[type=checkbox]:checked::before{
                    background-color: black !important;
    }
</style>
