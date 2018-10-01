<template>
    <div class="searchWrapper">
        <input
                id="search"
               name="search"
                :class="{ dark }"
               :value="value"
                @input="handleChange"
        />
    </div>
</template>

<script>
  export default {
    name: 'SearchInput',
    props: {
      value: {
        type: String,
        required: true,
      },
      dark: {
        type: Boolean,
        default: false,
      },
    },
    methods: {
      handleChange(e) {
        this.$emit('input', e.target.value);
      }
    }
  };
</script>

<style lang="scss" scoped>

    .searchWrapper {
        margin-top: 50px;
    }
        input {
            color: white;
            text-align: center;
            font-size: 18px;
            font-weight: 300;
            height: 30px;
            border: 0;
            border-bottom: 1px solid white;
            background: none;
            transition: box-shadow .5s ease-out;

            @media (min-width:768px) {
                font-size: 22px;
                letter-spacing: 1px;
            }
            @media (min-width:1024px) {
                font-size: 30px;
                font-weight: 400;
                letter-spacing: 1px;
            }
        }
        input:focus {
            outline: none;
            box-shadow: 0 10px 20px -8px rgba(255,255,255, .5);
        }

    .dark {
        color: #1e3d4a;
        border-bottom-color: #1e3d4a;
    }
    .dark:focus {
        box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
    }

</style>
