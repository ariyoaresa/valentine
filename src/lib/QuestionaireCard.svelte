<script lang="ts">
    let currentStepId = $state("0");
    const currentStep = $derived.by(
        () => steps.find((s) => s.id === currentStepId) || steps[0],
    );
    const steps = [
        {
            id: "0",
            questionText: "Hey pookie! You know what time it is",
            questionImage: "/1.gif",
            showActionButtons: true,
            yesButtonText: "yes, my love",
            yesButtonGotoStep: "closer",
            noButtonText: "i don't give a f",
            noButtonGotoStep: "1-no",
        },
        {
            id: "1-no",
            questionText: "I know i've been a bad boy, but is still want you",
            questionImage: "/2.gif",
            showActionButtons: true,
            yesButtonText: "i forgive you baby",
            yesButtonGotoStep: "1",
            noButtonText: "me i don't want you",
            noButtonGotoStep: "2",
        },
        {
            id: "closer",
            questionText: "I want to use this lover's season to let you know how special you are to me, Everyday is valentine's day with you",
            questionImage: "/6.gif",
            showActionButtons: true,
            yesButtonText: "Awwn, that's sweet baby",
            yesButtonGotoStep: "semi-final",
            noButtonText: "Just that?",
            noButtonGotoStep: "final-no",
        },
        {
            id: "semi-final",
            questionText: "Will you be my valentine?",
            questionImage: "/3.gif",
            showActionButtons: true,
            yesButtonText: "yes, and always",
            yesButtonGotoStep: "final-yes",
            noButtonText: "you wish",
            noButtonGotoStep: "final-no",
        },
        {
            id: "final-yes",
            questionText: "I love you pookie, Happy Valentines!",
            questionImage: "/4.gif",
            showActionButtons: false,
        },
        {
            id: "final-no",
            questionText: "I knew you'd say yes, Happy Valentines!",
            questionImage: "/5.gif",
            showActionButtons: false,
        },
    ];
    
    $effect(() => {
      if((currentStepId !== 'final-yes') && (currentStepId !== 'final-no')) return
      const defaults = {
        spread: 360,
        ticks: 100,
        gravity: 0,
        decay: 0.94,
        startVelocity: 30,
        shapes: ["heart"],
        colors: ["FFC0CB", "FF69B4", "FF1493", "C71585"],
      };
      confetti({
        ...defaults,
        particleCount: 50,
        scalar: 2,
      });
      
      confetti({
        ...defaults,
        particleCount: 25,
        scalar: 3,
      });
      
      confetti({
        ...defaults,
        particleCount: 10,
        scalar: 4,
      });
    })

    const gotoStep = (id: string) => (currentStepId = id);
</script>

<div class="container">
    <img class="img" src="/calendar.png" alt="valentine calendar" />
    <div class="component-container">
        <p class="question-text courgette-regular">
            {currentStep.questionText}
        </p>
        <img
            class="question-img"
            src={currentStep.questionImage}
            alt="it's about time"
        />
    </div>
    {#if currentStep.showActionButtons}
        <div class="action-button-container">
            <button
                onclick={() => gotoStep(currentStep.yesButtonGotoStep)}
                class="btn yes-btn courgette-regular"
                >{currentStep.yesButtonText}</button
            >
            <button
                onclick={() => gotoStep(currentStep.noButtonGotoStep)}
                class="btn no-btn courgette-regular"
                >{currentStep.noButtonText}</button
            >
        </div>
    {/if}
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        margin-block-start: -15vh;
        width: 90vw;
        min-height: 60vh;
        background: #c475a5;
        border-radius: 10px;
        box-shadow: 0 0 22px 8px rgba(0 0 0 / 0.1);
        position: relative;
        padding: 10px;
    }

    .component-container {
        padding-block-start: 70px;
        flex: 1;
    }

    .img {
        position: absolute;
        width: 100px;
        top: -15px;
        right: -5px;
        animation: pulse 2s infinite;
    }

    .question-text {
        color: #60123f;
        font-size: 1.3rem;
        padding-block-end: 0.75rem;
    }
    .question-img {
        display: block;
        object-fit: contain;
        max-width: 100%;
        border-radius: 5px;
        margin-inline: auto;
    }

    .action-button-container {
        display: flex;
        justify-content: center;
        margin-block-start: 10px;
        gap: 2rem;
    }

    .btn {
        padding: 5px 8px;
        border-radius: 5px;
        border-style: none;
        font-size: 1.3rem;
        font-weight: bold;
        color: #fff;
    }

    .yes-btn {
        background: green;
    }

    .no-btn {
        background: red;
    }

    @keyframes pulse {
        50% {
            transform: scale(1.1);
        }
    }
</style>
