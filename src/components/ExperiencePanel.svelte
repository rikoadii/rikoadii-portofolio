<script lang="ts">
  interface Experience {
    company: string;
    role: string;
    period: string;
    year: number;
    skills: string[];
  }

  interface Group {
    year: number;
    experiences: Experience[];
  }

  const experiences: Experience[] = [
    {
      company: "AISADEV",
      role: "Mobile Developer",
      period: "August 2025 – October 2025",
      year: 2025,
      skills: ["Dart", "Flutter", "Teamwork"],
    },
    {
      company: "CV. Victory Production",
      role: "Web Developer Intern",
      period: "July 2025 – August 2025",
      year: 2025,
      skills: ["PHP", "Javascript", "Tailwind.css", "React.js", "Teamwork"],
    },
    {
      company: "PT. Birodinamika Psikologis",
      role: "Mobile Developer",
      period: "December 2024 – December 2025",
      year: 2024,
      skills: ["Dart", "Flutter", "Teamwork"],
    },
    {
      company: "PT. Bisatopup Teknologi Indonesia",
      role: "Mobile Developer Intern",
      period: "November 2024 – December 2024",
      year: 2024,
      skills: ["Kotlin", "Jetpack Compose", "Teamwork"],
    },
    {
      company: "CV. DUAL RIZKI",
      role: "IT Support Intern",
      period: "Februari 2021 – April 2021",
      year: 2021,
      skills: ["Component Level Repair", "OS Deployment & Configuration", "Software Provisioning"],
    },
  ];

  const grouped = experiences.reduce(
    (acc, exp) => {
      if (!acc[exp.year]) {
        acc[exp.year] = [];
      }
      acc[exp.year].push(exp);
      return acc;
    },
    {} as Record<number, Experience[]>,
  );

  const groups: Group[] = Object.keys(grouped)
    .map((yearStr) => ({
      year: Number.parseInt(yearStr, 10),
      experiences: grouped[Number.parseInt(yearStr, 10)],
    }))
    .sort((a, b) => b.year - a.year);
</script>

<div class="card-base px-8 py-6">
  {#each groups as group}
    <div>
      <div class="flex flex-row w-full items-center h-[3.75rem]">
        <div
          class="w-[15%] md:w-[10%] transition text-2xl font-bold text-right text-75"
        >
          {group.year}
        </div>
        <div class="w-[15%] md:w-[10%]">
          <div
            class="h-3 w-3 bg-none rounded-full outline outline-[var(--primary)] mx-auto
                  -outline-offset-[2px] z-50 outline-3"
          ></div>
        </div>
        <div class="w-[70%] md:w-[80%] transition text-left text-50">
          {group.experiences.length}
          {group.experiences.length === 1 ? "position" : "positions"}
        </div>
      </div>

      {#each group.experiences as exp}
        <div
          class="group btn-plain !block w-full rounded-lg py-3 px-0"
        >
          <div class="flex flex-row justify-start items-center h-full">
            <!-- role -->
            <div
              class="w-[15%] md:w-[10%] transition text-sm text-right text-50"
            >
              <!-- empty for alignment -->
            </div>

            <!-- dot and line -->
            <div
              class="w-[15%] md:w-[10%] relative dash-line h-full flex items-center"
            >
              <div
                class="transition-all mx-auto w-1 h-1 rounded
                       bg-[oklch(0.5_0.05_var(--hue))]
                       outline outline-4 z-50
                       outline-[var(--card-bg)]"
              ></div>
            </div>

            <!-- experience info + skills -->
            <div class="w-[70%] md:w-[80%] text-left flex flex-col md:flex-row md:justify-between md:items-center">
              <div class="shrink-0">
                <div class="font-bold text-75 text-base">
                  {exp.role}
                </div>
                <div class="text-sm text-50 mt-0.5">
                  {exp.company}
                </div>
                <div class="text-xs text-30 mt-0.5">
                  {exp.period}
                </div>
              </div>
              <div class="flex flex-wrap gap-1.5 mt-2 md:mt-0 md:justify-end md:ml-4 md:max-w-[50%]">
                {#each exp.skills as skill}
                  <span class="text-xs px-2 py-0.5 rounded-md
                    bg-[var(--btn-plain-bg)] text-50
                    transition">
                    {skill}
                  </span>
                {/each}
              </div>
            </div>
          </div>
        </div>
      {/each}
    </div>
  {/each}
</div>
