<!-- u24666981 MOtheo Morena -->

<template>
    <section>
        <h2 id = "contact-title"> Contact Me </h2>
        <form name="contact" class = "contact-form">
            <p>
                <label>
                Name:<br>
                    <input type="text" name="name" required>
                </label>
            </p>
            <p>
                <label>
                Email:<br>
                    <input type="email" name="email" required>
                </label>
            </p>
            <p>
                <label>
                Message:<br>
                    <textarea name="message" required></textarea>
                </label>
            </p>
            <p>
                <button type="submit">Send</button>
            </p>
        </form>
    </section>
</template>

<script>

</script>

<style scoped>
    #contact-title {
        font-size: 2.5em;
        font-weight: bold;
        color: #fff;
        margin-bottom: 1.5rem;
        letter-spacing: 2px;
        transform: translateX(40%);
    }

    .contact-form {
        background: rgba(0, 0, 0, 0.6);
        border: 2px solid #fff;
        border-radius: 1rem;
        box-shadow: 0 0 15px rgba(0,0,0,0.3);
        padding: 2rem;
        max-width: 650px;
        color: #fff;
        margin: 0 auto 2rem auto;
        display: flex;
        flex-direction: column;
        gap: 1.2rem;
    }

    .contact-form label {
        color: #fff;
        font-size: 1.1em;
        font-weight: 500;
        letter-spacing: 1px;
    }

    .contact-form input,
    .contact-form textarea {
        width: 80%;
        padding: 0.7em 1em;
        margin-top: 0.5em;
        background: rgba(255,255,255,0.08);
        border: 1.5px solid #fff;
        border-radius: 0.5em;
        color: #fff;
        font-size: 1em;
        font-family: inherit;
        box-shadow: 0 0 5px rgba(0,0,0,0.14);
        transition: border-color 0.2s, box-shadow 0.2s;
    }

    .contact-form input:focus,
    .contact-form textarea:focus {
        outline: none;
        border-color: #61dafb;
        box-shadow: 0 0 8px #61dafb44;
    }

    .contact-form textarea {
        min-height: 90px;
        resize: vertical;
    }

    .contact-btn {
        background: #fff;
        color: #000;
        font-weight: bold;
        border: none;
        border-radius: 0.5em;
        padding: 0.7em 2em;
        font-size: 1.1em;
        cursor: pointer;
        box-shadow: 0 2px 8px rgba(0,0,0,0.12);
        transition: background 0.2s, color 0.2s;
    }

    .contact-btn:hover,
    .contact-btn:focus {
        background: #61dafb;
        color: #000;
    }
</style>