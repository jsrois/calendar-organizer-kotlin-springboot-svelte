<script>

    import Day from "./Day.svelte";

    const getAllDaysInMonth = (month, year) =>
        Array.from(
            {length: new Date(year, month, 0).getDate()},
            (_, i) => new Date(year, month - 1, i + 1)
        );

    const dayOfTheWeek = {
        0: "Monday",
        1: "Tuesday",
        2: "Wednesday",
        3: "Thursday",
        4: "Friday",
        5: "Saturday",
        6: "Sunday"
    };


    let days = getAllDaysInMonth(6, 2023)
        .map((d, i) => ({
            weekDay: d.getDay(),
            monthDay: i
        }))

    let fn = (acc, currentValue, _, originalArray) => {
        if (acc.length === 0) {
            let week = new Array(currentValue.weekDay)
            return [[...week, currentValue]]
        }

        if (currentValue.weekDay === 0) {
            return [...acc, [currentValue]];
        }
        let currentWeek = acc[acc.length - 1];
        currentWeek = [...currentWeek, currentValue];
        if (originalArray[originalArray.length - 1] === currentValue) {
            currentWeek = [...currentWeek, ...(new Array(6 - currentValue.weekDay))];
            console.log(currentWeek)
        }
        acc[acc.length - 1] = currentWeek;

        return acc;
    }

    let weeks = days.reduce(fn, [])

</script>
<section>
    {#each weeks as week}
        <div class="week">
            {#each week as day}
                <Day {day}/>
            {/each}
        </div>
    {/each}
</section>


<style>
    section {
        margin: auto;
    }

    .week {
        display: flex;
        justify-content: flex-start;
    }
</style>

