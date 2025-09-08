<template>
  <div class="input-futurista" :class="{ 'input-focado': isFocused }">
    <div class="field-container">
      <label :for="id" class="floating-label">
        <span class="label-text">{{ label }}</span>
        <span class="required-asterisk" v-if="required">*</span>
      </label>
      
      <div class="input-wrapper">
        <input
          :type="type"
          :id="id"
          :placeholder="isFocused ? placeholder : ''"
          :value="modelValue"
          @input="$emit('update:modelValue', $event.target.value)"
          @focus="isFocused = true"
          @blur="isFocused = false"
          :required="required"
          class="futurist-input"
        />
        
        <div class="input-highlight"></div>
        <div class="input-border"></div>
        
        <div class="icon-container" v-if="icon">
          <span class="input-icon" :class="icon"></span>
        </div>
      </div>
      
      <div class="hint-text" v-if="hint">{{ hint }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MeuComponenteFuturista',
  props: {
    label: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    id: {
      type: String,
      required: true
    },
    modelValue: {
      type: String,
      default: ''
    },
    required: {
      type: Boolean,
      default: false
    },
    hint: {
      type: String,
      default: ''
    },
    icon: {
      type: String,
      default: ''
    }
  },
  emits: ['update:modelValue'],
  data() {
    return {
      isFocused: false
    }
  }
}
</script>

<style scoped>
.input-futurista {
  margin-bottom: 1.8rem;
  position: relative;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.field-container {
  position: relative;
}

.floating-label {
  display: flex;
  align-items: center;
  margin-bottom: 0.6rem;
  font-weight: 600;
  font-size: 0.9rem;
  color: rgba(14, 71, 141, 0.85);
  text-shadow: 0 1px 2px rgba(216, 123, 18, 0.2);
  transition: all 0.3s ease;
}

.required-asterisk {
  color: #4c06e1;
  margin-left: 0.2rem;
  font-weight: bold;
}

.input-wrapper {
  position: relative;
  border-radius: 12px;
  background: rgba(9, 9, 184, 0.4);
  backdrop-filter: blur(10px);
  box-shadow: 
    inset 3px 3px 5px rgba(0, 0, 0, 0.2),
    inset -3px -3px 8px rgba(255, 255, 255, 0.07),
    0 8px 20px rgba(0, 0, 0, 0.3);
  transition: all 0.4s ease;
  overflow: hidden;
}

.input-focado .input-wrapper {
  box-shadow: 
    inset 3px 3px 5px rgba(0, 0, 0, 0.2),
    inset -3px -3px 8px rgba(255, 255, 255, 0.07),
    0 8px 25px rgba(100, 120, 255, 0.25);
  transform: translateY(-2px);
}

.futurist-input {
  width: 100%;
  padding: 1.2rem 1rem 0.8rem;
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.9);
  background: transparent;
  border: none;
  outline: none;
  position: relative;
  z-index: 2;
  transition: all 0.3s ease;
}

.futurist-input::placeholder {
  color: rgba(255, 255, 255, 0.4);
  font-style: italic;
}

.input-highlight {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #6e45e2, #88d3ce);
  transition: width 0.4s ease;
  z-index: 3;
}

.input-focado .input-highlight {
  width: 100%;
}

.input-border {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  pointer-events: none;
  box-shadow: 0 0 0 1px rgba(255, 255, 255, 0.05);
  transition: all 0.4s ease;
}

.input-focado .input-border {
  box-shadow: 0 0 0 1px rgba(110, 69, 226, 0.4);
}

.icon-container {
  position: absolute;
  right: 1rem;
  top: 50%;
  transform: translateY(-50%);
  z-index: 2;
  color: rgba(255, 255, 255, 0.5);
  transition: all 0.3s ease;
}

.input-focado .icon-container {
  color: #6e45e2;
}

.input-icon {
  font-size: 1.2rem;
}

.hint-text {
  margin-top: 0.5rem;
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.5);
  padding: 0 0.5rem;
  transition: all 0.3s ease;
}

.input-focado .hint-text {
  color: rgba(136, 211, 206, 0.8);
}

/* Animações */
@keyframes glow {
  0% { box-shadow: 0 0 5px rgba(110, 69, 226, 0.5); }
  50% { box-shadow: 0 0 20px rgba(110, 69, 226, 0.8); }
  100% { box-shadow: 0 0 5px rgba(110, 69, 226, 0.5); }
}

.input-futurista:focus-within {
  animation: glow 2s infinite;
}

/* Efeito de preenchimento automático */
.futurist-input:-webkit-autofill,
.futurist-input:-webkit-autofill:hover, 
.futurist-input:-webkit-autofill:focus {
  -webkit-text-fill-color: rgba(255, 255, 255, 0.9);
  -webkit-box-shadow: 0 0 0px 1000px rgba(30, 30, 45, 0.6) inset;
  transition: background-color 5000s ease-in-out 0s;
}
</style>