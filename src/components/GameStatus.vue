<template>
	<div class="gamestatus-container">
		<div v-if="this.started" class="info-container">
            <span>
                Hold <span class="enter">enter</span> to restart.
            </span>
        </div>
        <div v-else class="info-container">
            <span>
                Press any key to start.
            </span>
        </div>
	</div>
</template>

<script>
export default {
	name: "GameStatus",
    props: ['started'],
	emits: ["restart"]
}
</script>

<style scoped>
.info-container > span {
    opacity: 0.5;
}
.info-container span.enter {
    border: 1px solid white;
    border-radius: 0.4rem;
    padding: 1px 6px;
}
</style>
