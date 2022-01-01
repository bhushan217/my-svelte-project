<script>
import B2kCheckBox from '../../B2kCheckBox.svelte';
//import CheckBox from './CheckBox.svelte';
import RadioButton from './RadioButton.svelte';
import TextArea from './TextArea.svelte';
  
export let objAttributes = {};

const fieldComponents = {
    'cb': B2kCheckBox,
    'ta': TextArea,
    'rb': RadioButton
};
</script>
<div>
    <svelte:component this={fieldComponents[objAttributes.type]} objAttributes={objAttributes} {...objAttributes}/>
</div>
<style>
label { order: 2; }
input { order: 1; }
</style>