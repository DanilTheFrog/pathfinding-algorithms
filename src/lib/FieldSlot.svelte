<script lang="ts">
  import { FieldType } from "./enums";

        export let type: FieldType = FieldType.Field;
        export let pos: {x:number, y:number} | undefined = undefined;
        export let size: number = 50;
        const data = {
            "data-x": pos?.x,
            "data-y": pos?.y
        }



        function className(type: FieldType): string {
            switch(type) {
                case FieldType.Field: return "slot-empty"
                case FieldType.Wall: return "slot-wall"
                case FieldType.Destination: return "slot-destination"
                case FieldType.Step: return "slot-step"
                case FieldType.Start: return "slot-start"
                default: {
                    console.warn("Used wrong type at FieldSlot: " + type);
                    return "slot-empty"
                }
            }

        }

        function getSize(s: number): string {
            return `width:${s}px;height:${s}px`
        }

        export function changeType(t: FieldType) {
            type = t;
        }
</script>

<style>
    .slot {
        width: 50px;
        height: 50px;
        border: 1px solid black;
        transition: 50ms;
    }
    .slot:hover {
        filter: brightness(1.2);

    }
    .slot-empty {
        background: var(--slot-field);
    }
    .slot-wall {
        background: var(--slot-wall);
    }
    .slot-destination {
        background: var(--slot-destination);
    }
    .slot-step {
        background: var(--slot-step);
    }
    .slot-start {
        background: var(--slot-start);

    }

</style>

<div class={`slot ${className(type)}`} style={`${getSize(size)}`} {...data}>

</div>