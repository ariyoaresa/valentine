<script lang="ts">
    import QuestionaireCard from "./lib/components/QuestionaireCard.svelte"
    import {base64Encode} from "./lib/utils/base64Parser";

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

    const {pathname} = window.location;
    if (pathname.startsWith("/encode")) {
        const name = pathname.replace("/encode", "");
        const encodedName = base64Encode(name);
        window.location.href = `${window.location.origin}/${encodedName}`
    }


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
