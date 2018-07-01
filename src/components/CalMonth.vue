<script>
import { monthNames, weekDayNames } from "../config/config.js";

export default {
  name: "cal-month",
  props: {
    month: {
      type: Number,
      default: 0
    },
    year: {
      type: Number,
      default: 0
    }
  },
  methods: {
    testaclick(evt) {
      evt.preventDefault();
      let date = evt.target.date;
      console.log(date);
    }
  },
  render: function(createElement) {
		let children = [];
		let today = new Date();
    let startDate = new Date(this.year, this.month, 1); // primeiro dia do mês
    let endOfMonth = new Date(this.year, this.month + 1, 0); // fim do mês
    let endOfPreviousMonth = new Date(this.year, this.month, 0); // fim do mês anterior

    // gerar a linha de headr com o nome do mês
    children.push(
      createElement("span", { class: "day grow" }, monthNames[this.month])
    );

    // Gerar linha de header com os nomes dos dias da semana
    for (var weekDay of weekDayNames) {
      children.push(createElement("span", { class: "day" }, weekDay));
    }

    // Padding até ao dia da semana correspondente ao início do mês actual
    for (let j = 1; j <= endOfPreviousMonth.getDay(); j++) {
      children.push(createElement("span", { class: "day" }, ""));
    }

    for (let dayNumber = 1; dayNumber <= endOfMonth.getDate(); dayNumber++) {
				let classes = ['day'];

			// gerar o dia para efeitos de cálculo
			let day = new Date(this.year, this.month, dayNumber);

			// validar se é um finm-de-semana
			if (day.getDay() === 0 || day.getDay() === 6) {
				classes.push('weekend');
			}

			// validar se este é do dia 
			console.log(day, today);
			if (day.toLocaleDateString() == today.toLocaleDateString()) {
				classes.push('today');
			}

			// validar se é uma data no passado
			if (day < today) {
				classes.push('past');
			}

      children.push(
        createElement( "a",
          {
            attrs: {
              href: "#"
            },
            class: classes.join(' '),
            on: {
              click: this.testaclick
            }
          },
          dayNumber < 10 ? `0${dayNumber}` : dayNumber
        )
      );
    }

    // Padding para fazer o próximo mês começar na linha seguinte
    for (let k = endOfMonth.getDay() + 1; k <= 7; k++) {
      children.push(createElement("span", { class: "day" }, ""));
    }

    return createElement(
      "div", // tag name
      { class: "month" },
      children // array of children
    );
  }
};
</script>

<style scoped>
a {
  color: #42b983;
	text-decoration: none;
}

.month {
  display: flex;
  justify-content: flex-start;
  flex-direction: row;
  flex-wrap: wrap;
  box-sizing: border-box;
	width: 300px;
	padding: 20px;
}

.day {
  width: calc(100% / 7);
  box-sizing: border-box;
  align-content: stretch;
  line-height: 20px;
  text-align: center;
}

.day.grow {
  width: 100%;
  flex-grow: 7;
  text-align: center;
  font-weight: bold;
}

.day.weekend {
  color: silver;
}

.day.past {
  color: blue;
}

.day.today {
  color: red;
	font-weight: bold;
}
</style>
