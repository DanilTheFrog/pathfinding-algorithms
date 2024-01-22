<script lang="ts">
  import Field from './lib/Field.svelte';
  import Settings from './lib/Settings.svelte';
  import { FieldType } from './lib/enums';
  const fieldInitial: FieldType[][] = [
    [FieldType.Field, FieldType.Step, FieldType.Step, FieldType.Step, FieldType.Field],
    [FieldType.Field, FieldType.Wall, FieldType.Wall, FieldType.Step, FieldType.Field],
    [FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Field],
    [FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Field],
    [FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Field, FieldType.Destination],

  ]

  let field: Field;
  let settings: Settings;

  function fieldClickHandler(e: MouseEvent) {
    e.preventDefault();
    e.stopPropagation();
    const target = e.target as HTMLInputElement;
    const x = target.getAttribute('data-x');
    const y = target.getAttribute('data-y');
    if(!x || !y) return;

    field.changeField(settings.state.selectedBrush, Number(x), Number(y))

  }
</script>

<style>
  .wrapper {
    display: flex;
  }
  .field {
    width: 100%;
    height: 100%;
    margin: auto;
  }
</style>

<main>
  <div class="wrapper">
    <Settings bind:this={settings}/>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div class="field" on:click={fieldClickHandler}>
      <Field size={settings?.state.size.x ? settings.state.size.x : 5} field={fieldInitial} bind:this={field}/>
    </div>

  </div>

</main>


