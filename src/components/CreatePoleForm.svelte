<script>
    import Button from '../shared/Button.svelte';

    let feilds = {question: '', answerA: '', answerB: ''}
    let errors = {question: '', answerA: '', answerB: ''}
    let valid = false;

    const submitHandler = () => {
        valid = true;

        if (feilds.question.trim().length < 5) {
            errors.question = 'Question must be at least 5 characters long';
            valid = false;
        } else {
            errors.question = '';
        }

        if (feilds.answerA.trim().length < 1) {
            errors.answerA = 'Answer must be greater than 1 character';
            valid = false;
        } else {
            errors.answerA = '';
        }

        if (feilds.answerB.trim().length < 1) {
            errors.answerB = 'Answer must be greater than 1 character';
            valid = false;
        } else {
            errors.answerB = '';
        }

        // Add new poll
        if (valid) {
            console.log('valid ' + feilds)
        }
        
    }
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question</label>
        <div class="form-input">
            <div class="errors">{errors.question}</div>
            <input type="text" id="question" class:red={errors.question > 1} bind:value={feilds.question} placeholder="Do you like dogs?">
        </div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A</label>
        <div class="form-input">
            <div class="errors">{errors.answerA}</div>
            <input type="text" id="answer-a" bind:value={feilds.answerA} placeholder="Yes!">
        </div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B</label>
        <div class="form-input">
            <div class="errors">{errors.answerB}</div>
            <input type="text" id="answer-b" bind:value={feilds.answerB} placeholder="No :(">
        </div>
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
            label {
                    user-select: none;
                    display: block;
                    font-size: 1.25rem;
                    font-weight: 100;
                    color: #555;
                    // padding-bottom: 15px;
                    text-align-last: left;
                }
            .form-input {
                input {
                    display: flex;
                    flex-direction: column;
                    align-items: center;
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
            }
        }
    }

    .errors { 
        color: #f00;
        font-size: 0.75rem;
        display: inline-block;
    }
</style>