<script lang="ts">
    import QuestionaireCard from "./lib/QuestionaireCard.svelte"

    const images = [
        "/1.gif",
        "/2.gif",
        "/3.gif",
        "/4.gif",
        "/5.gif",
        "/6.gif",
    ];

    images.forEach(src => {
        const img = new Image();
        img.src = src;
    });

</script>

<main>
    <QuestionaireCard />
</main>

<style>
main {
    display: grid;
    place-content: center;
    background: url('/bg.jpg');
    width: 100%;
    height: 100dvh;
}
</style>
