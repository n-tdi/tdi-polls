<script>
    import Button from '../shared/Button.svelte';

    let fields = {question: '', answerA: '', answerB: ''}
    const submitHandler = () => {
        console.log(fields)
    }
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" id="question" bind:value={fields.question} placeholder="Do you like dogs?">
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A</label>
        <input type="text" id="answer-a" bind:value={fields.answerA} placeholder="Yes!">
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B</label>
        <input type="text" id="answer-b" bind:value={fields.answerB} placeholder="No :(">
    </div>
    <Button inverse={true}>Add Poll</Button>
</form>

<style lang="scss">
    form {
        width: 400px;
        margin: 0 auto;
        text-align: center;
        .form-field {
            margin: 18px;
            input {
                width: 100%;
                border: 1px solid #ccc;
                border-radius: 4px;
                padding: 8px;
                font-size: 1.25rem;
                font-weight: 100;
                color: #555;
                &:focus {
                    outline: none;
                    border-color: #3890ce;
                }
            }
            label {
                display: block;
                font-size: 1.25rem;
                font-weight: 100;
                color: #555;
                padding-bottom: 15px;
                text-align-last: left;
            }
        }
    }
</style>