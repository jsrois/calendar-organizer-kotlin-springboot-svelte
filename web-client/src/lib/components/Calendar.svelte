<script>

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

    let fn = (acc, currentValue) => {
        if (acc.length === 0) {
            console.log(".")
            let week = new Array(currentValue.weekDay)
            return [[...week, currentValue]]
        }

        if (currentValue.weekDay === 0) {
            console.log("x")
            return [...acc, [currentValue]];
        }
        let currentWeek = acc[acc.length - 1];
        currentWeek = [...currentWeek, currentValue];
        acc[acc.length - 1] = currentWeek;
        console.log('o');
        return acc;
    }

    let datesOrganized = days.reduce(fn, [])

</script>
<section>
    {#each datesOrganized as week}
        <div class="week">
            {#each week as day}
                {#if day}
                    <div class="day">{day.monthDay + 1}</div>
                {:else }
                    <div class="day empty"></div>
                {/if}
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

    .day {
        width: 100px;
        height: 100px;
        border: 1px solid black;
    }
</style>

