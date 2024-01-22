<script lang="ts">
  import type { ChangeEventHandler } from "svelte/elements";
  import FieldSlot from "./FieldSlot.svelte";
  import { FieldType } from "./enums";
    type SettingsProps = {
        minFieldSize: number;
        maxFieldSize: number;
    }
    export let settingsProps: SettingsProps = {
        minFieldSize: 5,
        maxFieldSize: 20
    }

  type TState = {
    disabled: boolean;
    selectedBrush: FieldType;
    size: {
        x: number;
        y: number;
    }
  }


  const brushInputs: Array<[string, FieldType]> = [
        ["Field", FieldType.Field], ["Wall", FieldType.Wall], ["Start", FieldType.Start], ["Destination", FieldType.Destination]
    ];

    
    export const state:TState = {
        selectedBrush: 0,
        size: {
            x:5,
            y:5
        },
        disabled: false
    } 

    //preventing unvalid value from bind:value
    const sizeChangeHandler: ChangeEventHandler<HTMLInputElement> = (e) => {
        const target = e.currentTarget;
        const val = Number(target.value);
        if(!(target.dataset.for === "x" || target.dataset.for === "y")) return;
        
        if(val < settingsProps.minFieldSize) state.size[target.dataset.for] = settingsProps.minFieldSize;
        if(val > settingsProps.maxFieldSize) state.size[target.dataset.for] = settingsProps.maxFieldSize;

        
    }
</script>

<style>
    .settings {
        background-color: rgb(187, 187, 187);
        width: 400px;
        height: 80%;
    }
    .select-item, label {
        width: 200px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        padding: 2;
        margin-top: 5px;
        margin-left: 4px;
    }

    label.field-size {
        font-size: 24px;
    }

    input.field-size{
        font-size: 18px;
    }


</style>

<div class="settings">
    <div>
  
        <fieldset class="pick-element" disabled={state.disabled}>
            <h3>
                Pick an element
            </h3>
            {#each brushInputs as b}
                <div class="select-item">

                    <input type="radio" id={`brush-${b[0]}`} name="brush-type" value={b[1]} checked bind:group={state.selectedBrush}>
                    <label for={`brush-${b[0]}`}> {b[0]} <FieldSlot size={30} type={b[1]}/></label><br>
                </div>
            {/each}
            <h4>
                Selected {state.selectedBrush}
            </h4>
        </fieldset>

        <fieldset>
            <h3>Set field size</h3>
            <div class="select-item">
                <label class="field-size" for="field-size-x">x</label>
                <input class="field-size" 
                type="number" id="field-size-x" 
                data-for={"x"}
                min="5" max="20" 
                bind:value={state.size.x} 
                on:change={sizeChangeHandler}>
            </div>

            <div class="select-item">
                <label class="field-size" for="field-size-y">y</label>
                <input class="field-size" 
                type="number" 
                id="field-size-y" 
                data-for="y" 
                min="5" max="20" 
                bind:value={state.size.y} on:change={sizeChangeHandler}>
            </div>

        </fieldset>


    </div>
</div>