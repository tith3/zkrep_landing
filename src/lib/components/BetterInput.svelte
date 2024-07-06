<script lang="ts">
    import { Icon, ExclamationTriangle, XCircle, Eye, EyeSlash } from "svelte-hero-icons";
  
    export let value = ""; // Exports the value for binding
    export let placeholder = ""; // Exports placeholder to set it dynamically
    export let errorText = ""; // Exports error text to show when error occurs
    export let inputType: InputType = "text"; // Exports password to toggle password mode
    export let onEnter = () => {}; // Exports onEnter function to handle enter key press
  
    type InputType = "text" | "password" | "tel" | "code";
    let type = inputType === "password" ? "password" : inputType; // Adjust type based on inputType
    let error = false;
    let errorValue = ""; // Tracks the error state
    let focused = false; // Tracks focus state of the input
  
    let inputElement: HTMLInputElement; // Reference to the input element
  
    function clearInput() {
      value = "";
      inputElement.focus(); // Refocus the input after clearing
    }
  
    function handleKeyDown(event: { key: string }) {
      if (event.key === "Enter") {
        onEnter();
      }
    }
  
    function formatPhoneNumber(value: string): string {
        const cleaned = value.replace(/\D/g, "").slice(0, 10); // Remove non-digit characters and limit to 10 digits
        const match = cleaned.match(/^(\d{0,3})(\d{0,3})(\d{0,4})$/);
        if (match) {
        return `${match[1] ? `(${match[1]}` : ""}${match[2] ? `) ${match[2]}` : ""}${match[3] ? `-${match[3]}` : ""}`;
        }
        return value;
    } 
    function formateVerificationCode(value: string): string {
        const cleaned = value.replace(/\D/g, "").slice(0, 6); // Remove non-digit characters and limit to 6 digits
        return cleaned;
    }
    function handleInput(event: Event) {
      const target = event.target as HTMLInputElement;
      if (inputType === "tel") {
        value = formatPhoneNumber(target.value);
      }
      if (inputType === "code"){
        value = formateVerificationCode(target.value);
      }
    }
  
    $: {
      if (errorText != "") {
        errorValue = value;
        error = true;
      } else {
        errorValue = "";
      }
    }
  
    $: {
      if (value != errorValue && error) {
        errorText = "";
        error = false;
        errorValue = "";
      }
    }
  
    $: {
      if (inputType != "password" && inputType != "tel") {
        type = "text";
      }
    }
  </script>
  
  <div class="w-full">
    <div
      class="input-wrapper w-full flex rounded-token border-token {error ? 'border-error-400-500-token' : (focused ? 'border-secondary-500' : 'border-surface-300-600-token dark:border-surface-500-400-token')}"
    >
      <input
        class="input py-2.5"
        {...{ type }}
        bind:this={inputElement}
        bind:value={value}
        placeholder=" "
        on:focus={() => (focused = true)}
        on:blur={() => (focused = false)}
        on:keydown={handleKeyDown}
        on:input={handleInput}
      />
      <!-- svelte-ignore a11y-label-has-associated-control -->
      <label class="input-label line-clamp-1">{placeholder}</label>
      <button
        on:click|preventDefault={() => {
          clearInput();
        }}
        class="btn-icon my-auto flex flex-row justify-center align-center {error ? 'visible opacity-100' : (focused && value ? 'visible opacity-100' : 'invisible opacity-0')}"
      >
        {#if error}
          <Icon src="{ExclamationTriangle}" size="20" class="text-error-500" />
        {:else}
          <Icon src="{XCircle}" size="20" />
        {/if}
      </button>
      {#if inputType === "password"}
        <button
          on:click|preventDefault={() => {
            if (type === "password") {
              type = "text";
            } else {
              type = "password";
            }
          }}
          class="btn-icon my-auto flex flex-row justify-center align-center"
        >
          <Icon src="{type === 'password' ? Eye : EyeSlash}" size="20" />
        </button>
      
      {/if}
      
    </div>
    {#if error}
      <p class="font-urbana text-sm px-2 text-error-500">{errorText}</p>
    {/if}
  </div>
  
  <style>
    .btn-icon {
      transition: all 0.2s ease;
      height: 100%;
    }
  
    .input-wrapper {
      transition: all 0.2s ease;
      position: relative;
    }
  
    .input {
      background-color: var(--surface-50-900);
      border: none;
      width: 100%;
      padding-top: 1rem;
      padding-bottom: 0.25rem;
    }
  
    .input-label {
      position: absolute;
      left: 0.75rem;
      top: 0.625rem;
      pointer-events: none;
      opacity: 0.5;
      transition: all 0.2s ease;
      transform-origin: left top;
    }
  
    .input:focus + .input-label,
    .input:not(:placeholder-shown) + .input-label {
      transform: scale(0.75) translateY(-10px);
    }
  
    ::-ms-reveal {
      display: none;
    }
  </style>
  