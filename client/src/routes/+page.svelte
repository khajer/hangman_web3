<script>
    const ANSWER_WORDS = "japan";
    var input_time = 0;
    var textfield = "";

    function check_word(text_input) {
        if (text_input === ANSWER_WORDS) {
            return true;
        }
        return false;
    }
    function check_answer() {
        input_time += 1;
    }

    function key_press(input) {
        textfield += input.key;
        var input_id = input.target.id;
        var id_num = parseInt(
            input_id.substring(input_id.length - 1, input_id.length)
        );
        console.log(id_num);
        if (id_num < 5) {
            id_num += 1;
            document.getElementById("input" + id_num).focus();
        } else {
            check_answer();
        }
    }
</script>

<h1>HangMan Over</h1>

<input type="text" maxlength="1" size="1" id="input1" on:keypress={key_press} />
<input type="text" maxlength="1" size="1" id="input2" on:keypress={key_press} />
<input type="text" maxlength="1" size="1" id="input3" on:keypress={key_press} />
<input type="text" maxlength="1" size="1" id="input4" on:keypress={key_press} />
<input type="text" maxlength="1" size="1" id="input5" on:keypress={key_press} />
