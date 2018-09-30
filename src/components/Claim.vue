<template>
    <div class="claimWrapper">
        <h1 class="claim"> SPACER </h1>
        <p class="subclaim">
            Begin your journey through our amazing galaxy and discover places you never even heard of.
        </p>
        <p class="subclaim">
            Type anything space-related to start.
        </p>
    </div>
</template>

<script>
  export default {
    name: 'Claim'
  };
</script>

<style lang="scss" scoped>
    .claimWrapper {
        text-align: center;
        diplay: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: white;
    }
    .claim {
        font-size: 50px;
        font-weight: 800;
        margin: 0;

        @media (min-width:768px) {
            font-size: 80px;
        }
        @media (min-width:1024px) {
            font-size: 120px;
            letter-spacing: 2px;
        }
    }
    .subclaim {
        margin: 20px 0 0 0;
        font-size: 13px;
        font-weight: 400;

        @media (min-width:768px) {
            font-size: 17px;
            letter-spacing: 1px;
            width: 500px;
        }

        @media (min-width:1024px) {
            font-size: 24px;
            letter-spacing: 1px;
        }
    }
</style>
