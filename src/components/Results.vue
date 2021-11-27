<template>
    <div class="result-container">
        <p><i class="fas fa-redo"></i>Tour {{ turn }}</p>

        <p v-if="paire < 2">
            <i class="fas fa-check-double"></i> 
            {{ paire }} paire trouvée
        </p>
        
        <p v-if="paire > 1">
            <i class="fas fa-check-double"></i> 
            {{ paire }} paires trouvées
        </p>
        
    </div>
</template>

<script>
export default {
    props: ['turn', 'paire']
}
</script>

<style scoped>
.result-container {
    margin: 20px auto;
    padding: 4px;
    width: 30%;
    border-radius: 10px;
    background-color: rgba(255, 255, 255, .9);
    text-align: left;
}
p {
    margin-left: 30px;
    font-size: 1.5rem;
    color: #6034CF;
}
i {
    margin: 0 10px;
}
</style>