<script>
    import Header from "./header.svelte";

    const BACKSPACE_KEY = 8;
    const ANSWER_WORDS = "japan";
    var textfield = "";
    var result = "";
    var cnt_play = 0;
    var imgHangman = "";
    var tmp_answer_text = "";

    var hangmans = [
        [" -----", "      |", "      |", "      |", "      |"],
        [" -----", "  |   |", "  o   |", "      |", "      |"],
        [" -----", "  |   |", "  o   |", " /|\\  |", "      |"],
        [" -----", "  |   |", "  o   |", " /|\\  |", " / \\  |"],
    ];

    function draw_image(lvl) {
        return hangmans[lvl - 1].join("<br>");
    }
    function check_word(text_input) {
        if (text_input === ANSWER_WORDS) {
            return true;
        }
        return false;
    }
    function check_answer(txt_answer) {
        cnt_play += 1;
        tmp_answer_text = textfield;
        if (check_word(txt_answer)) {
            result = "YOU WIN";
        } else {
            clear_all_text();
            if (cnt_play < 4) {
                console.log(cnt_play);
                imgHangman = draw_image(cnt_play);
            } else {
                result = "YOU LOSE";
            }
            textfield = "";
        }
    }
    function clear_all_text() {
        for (var i = 1; i <= 5; i++) {
            document.getElementById("input" + i).value = "";
        }
    }

    function key_press(input) {
        textfield += input.key;

        if (textfield.length == 5) {
            tmp_answer_text = "";
        }
        var input_id = input.target.id;
        var id_num = parseInt(
            input_id.substring(input_id.length - 1, input_id.length)
        );
        if (id_num < 5) {
            id_num += 1;
            document.getElementById("input" + id_num).focus();
        } else {
            document.getElementById("input" + id_num).blur();
            check_answer(textfield);
        }
    }

    function key_up(input) {
        if (input.keyCode == BACKSPACE_KEY) {
            var input_id = input.target.id;
            var id_num = parseInt(
                input_id.substring(input_id.length - 1, input_id.length)
            );
            if (id_num > 1) {
                id_num -= 1;
                var val = document.getElementById("input" + id_num).value;
                document.getElementById("input" + id_num).focus();

                document.getElementById("input" + id_num).value = val;
            }
        }
    }
</script>

<Header />
<h1>HangMan Over</h1>
what is country beautiful on asia?
<br />
{@html imgHangman}
<br />
<input
    type="text"
    maxlength="1"
    size="1"
    id="input1"
    on:keypress={key_press}
    on:keyup={key_up}
/>
<input
    type="text"
    maxlength="1"
    size="1"
    id="input2"
    on:keypress={key_press}
    on:keyup={key_up}
/>
<input
    type="text"
    maxlength="1"
    size="1"
    id="input3"
    on:keypress={key_press}
    on:keyup={key_up}
/>
<input
    type="text"
    maxlength="1"
    size="1"
    id="input4"
    on:keypress={key_press}
    on:keyup={key_up}
/>
<input
    type="text"
    maxlength="1"
    size="1"
    id="input5"
    on:keypress={key_press}
    on:keyup={key_up}
/>
<br />
answer = "{tmp_answer_text}"
<h2>{result}</h2>
