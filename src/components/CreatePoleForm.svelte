<script>
    import PollStore from '../stores/PollStore.js';
    import { createEventDispatcher } from "svelte";
    import crypto from "crypto";
    import Card from '../shared/Card.svelte';
    let dispatch = createEventDispatcher();
    import Button from '../shared/Button.svelte';
    'use strict';

    let feilds = {question: '', answerA: '', answerB: ''};
    let errors = {question: '', answerA: '', answerB: ''};
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
            errors.answerA = 'Answer A must be greater than 1 character';
            valid = false;
        } else {
            errors.answerA = '';
        }

        if (feilds.answerB.trim().length < 1) {
            errors.answerB = 'Answer B must be greater than 1 character';
            valid = false;
        } else {
            errors.answerB = '';
        }

        // Add new poll
        if (valid) {
            let poll = {...feilds, votesA: 0, votesB: 0, id: Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15)};
            // Save poll to store

            PollStore.update((data) => {
                return [poll, ...data];
            });
            dispatch('addPoll');
        }    
    };

    const handleClick = (object) => {
        if (object.length > 1) {
            for (const [key, value] of Object.entries(errors)) {
                if (errors[key] === object) {
                    errors[key] = '';
                    break;
                }
            }
        }
    };
</script>

<div class="main">
    <div class="left">
        <form on:submit|preventDefault={submitHandler}>
            <div class="form-field">
                <label for="question">Poll Question</label>
                <div class="form-input">
                    <div class="errors">{errors.question}</div>
                    <input type="text" id="question" on:click={() => handleClick(errors.question)} class:red={errors.question > 1} bind:value={feilds.question} placeholder="Do you like dogs?">
                </div>
            </div>
            <div class="form-field">
                <label for="answer-a">Answer A</label>
                <div class="form-input">
                    <div class="errors" >{errors.answerA}</div>
                    <input type="text" id="answer-a" on:click={() => handleClick(errors.answerA)} bind:value={feilds.answerA} placeholder="Yes!">
                </div>
            </div>
            <div class="form-field">
                <label for="answer-b">Answer B</label>
                <div class="form-input">
                    <div class="errors">{errors.answerB}</div>
                    <input type="text" id="answer-b" on:click={() => handleClick(errors.answerB)} bind:value={feilds.answerB} placeholder="No :(">
                </div>
            </div>
            <Button inverse={true}>Add Poll</Button>
        </form>
    </div>
    <div class="right">
        <Card>
            <div class="poll">
                <h3>{feilds.question}</h3>
                <p>Total Votes: 7</p>
                <div class="answer">
                    <div class="percent percent-a" style="width: 71%"></div>
                    <span>{feilds.answerA} (5)</span>
                </div>
                <div class="answer">
                    <div class="percent percent-b" style="width: 29%"></div>
                    <span>{feilds.answerB} (2)</span>
                </div>
            </div>
        </Card>
    </div>
</div>

<style lang="scss">
    .main {
        display: grid;
        grid-template-columns: 1fr 1fr;
        .left {
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
                background-color: #fff;
                font-size: 0.75rem;
                display: inline-block;
                position: relative;
                top: 7px;
                padding: 0 5px;
            }
        }
        .right {
            .poll {
                user-select: none;
                h3 {
                    margin: 0 auto;
                    color: #555;
                }
                p {
                    margin-top: 6px;
                    font-size: 14px;
                    color: #aaa;
                    margin-bottom: 30px;
                }
                .answer {
                    background-color: #fafafa;
                    cursor: pointer;
                    margin: 10% auto;
                    position: relative;
                    :hover {
                        opacity: 0.6;
                    }
                    span {
                        display: inline-block;
                        padding: 10px 20px;
                    }
                    .percent {
                        height: 100%;
                        position: absolute;
                        box-sizing: border-box;

                    }
                    .percent-a {
                        border-left: 4px solid #d91b42;
                        background-color: rgba(217, 27, 66, 0.2);
                    }
                    .percent-b {
                        border-left: 4px solid #1b9e6a;
                        background-color: rgba(0, 188, 212, 0.2);
                    }
                }
                .delete {
                    margin-top: 30px;
                    text-align: center;
                }
            }
        }
    }
</style>