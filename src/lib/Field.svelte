<script lang="ts">
    import FieldSlot from "./FieldSlot.svelte";
    import { FieldType } from "./enums";


    export let size = 3;
    export let field:FieldType[][] = new Array(size).fill(FieldType.Field).map(()=> new Array(size).fill(FieldType.Field));
    const elements: any = new Array(size).fill(null).map(()=> new Array(size).fill(null));

    export function changeField(type: FieldType, x: number, y: number): void {
        field[x][y] == type;
        elements[x][y].changeType(type);
    }

</script>

<style>
    .field-row {
        display: inline-block;
    }
    .field {
        display: block;
    }
</style>

<div class="field" >
    {#each Array(size) as r, i}
        <div class="field-row">
            {#each Array(size) as c, j}
                <FieldSlot type={field[j][i]} bind:this={elements[i][j]} pos={{x:i, y:j}}/>
            {/each}
        </div>
    {/each}
</div>