

<div class="section">
</div>
<p>
    Scroll to Explore all the Scores
</p>

<style>
    .section {
        /* background: #333; */
        height: 60px;
        position: relative;
        width: 100%;
    }

    .section::before {
        animation: bounce 2s ease infinite;
        bottom: 1rem;
        /* color: #111; */
        content: '╲╱';
        font-size: 0.8rem;
        height: 2rem;
        left: 50%;
        letter-spacing: -1px;
        line-height: 4rem;
        margin-left: -3rem;
        position: absolute;
        text-align: center;
        width: 6rem;
    }

    p {
        animation: bounce 2s ease infinite;
    }

    @keyframes bounce {
        50% {
            transform: translateY(-50%);
        }
    }

    p {
        font-size: 14px;
    }
</style>
