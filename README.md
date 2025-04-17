#include <stdio.h>
#include <stdlib.h>

#define NUM_CANDIDATES 6
#define MAX_STR 100

int calculate_age(int year, int month, int day) {
    int current_year = 2025, current_month = 4, current_day = 10;
    int age = current_year - year;
    if (month > current_month || (month == current_month && day > current_day)) {
        age--;
    }
    return age;
}

int main() {
    char group_name[MAX_STR];
    char c;
    int i;

    // Candidate arrays
    char candidate01[MAX_STR], candidate02[MAX_STR], candidate03[MAX_STR];
    char candidate04[MAX_STR], candidate05[MAX_STR], candidate06[MAX_STR];

    // Data storage arrays
    char member_info[NUM_CANDIDATES][11][MAX_STR];
    int birth_year[NUM_CANDIDATES], birth_month[NUM_CANDIDATES], birth_day[NUM_CANDIDATES];
    int age[NUM_CANDIDATES];

    // Get group name using getchar()
    printf("Enter Audition Group Name: ");
    int idx = 0;
    while ((c = getchar()) != '\n' && idx < MAX_STR - 1) {
        group_name[idx++] = c;
    }
    group_name[idx] = '\0';

    printf("####################################\n");
    printf("[%s] Audition Candidate Data Entry\n", group_name);
    printf("####################################\n");

    i = 0;
    while (i < NUM_CANDIDATES) {
        printf("Entering information for candidate %d.\n", i + 1);
        printf("---------------------------------\n");

        printf("1. Name: ");
        fgets(member_info[i][0], MAX_STR, stdin);
        member_info[i][0][strcspn(member_info[i][0], "\n")] = '\0';

        printf("2. Date of Birth (YYYY/MM/DD format): ");
        scanf("%d/%d/%d", &birth_year[i], &birth_month[i], &birth_day[i]);
        getchar();

        printf("3. Gender (F for Female, M for Male): ");
        fgets(member_info[i][2], MAX_STR, stdin);
        member_info[i][2][strcspn(member_info[i][2], "\n")] = '\0';

        printf("4. Email: ");
        fgets(member_info[i][3], MAX_STR, stdin);
        member_info[i][3][strcspn(member_info[i][3], "\n")] = '\0';

        printf("5. Nationality: ");
        fgets(member_info[i][4], MAX_STR, stdin);
        member_info[i][4][strcspn(member_info[i][4], "\n")] = '\0';

        printf("6. BMI: ");
        fgets(member_info[i][5], MAX_STR, stdin);
        member_info[i][5][strcspn(member_info[i][5], "\n")] = '\0';

        printf("7. Primary Skill: ");
        fgets(member_info[i][6], MAX_STR, stdin);
        member_info[i][6][strcspn(member_info[i][6], "\n")] = '\0';

        printf("8. Secondary Skill: ");
        fgets(member_info[i][7], MAX_STR, stdin);
        member_info[i][7][strcspn(member_info[i][7], "\n")] = '\0';

        printf("9. Korean Proficiency Level (TOPIK): ");
        fgets(member_info[i][8], MAX_STR, stdin);
        member_info[i][8][strcspn(member_info[i][8], "\n")] = '\0';

        printf("10. MBTI: ");
        fgets(member_info[i][9], MAX_STR, stdin);
        member_info[i][9][strcspn(member_info[i][9], "\n")] = '\0';

        printf("11. Introduction: ");
        fgets(member_info[i][10], MAX_STR, stdin);
        member_info[i][10][strcspn(member_info[i][10], "\n")] = '\0';

        age[i] = calculate_age(birth_year[i], birth_month[i], birth_day[i]);

        printf("=================================\n");
        i++;
    }

    // Output
    printf("\n####################################\n");
    printf("[%s] Audition Candidate Data Review\n", group_name);
    printf("####################################\n");
    printf("=============================================================================================\n");
    printf("Name (Age)        | DOB       | Gender | Email               | Nationality | BMI  | Primary Skill | Secondary Skill | TOPIK | MBTI |\n");
    printf("=============================================================================================\n");

    for (i = 0; i < NUM_CANDIDATES; i++) {
        printf("%-16s (%d) | %04d%02d%02d | %-6s | %-20s | %-12s | %-4s | %-13s | %-15s | %-5s | %-4s |\n",
            member_info[i][0],
            age[i],
            birth_year[i], birth_month[i], birth_day[i],
            member_info[i][2],
            member_info[i][3],
            member_info[i][4],
            member_info[i][5],
            member_info[i][6],
            member_info[i][7],
            (atoi(member_info[i][8]) == 0 ? "Native" : member_info[i][8]),
            member_info[i][9]
        );
        printf("-------------------------------------------------------------------------------------\n");
        printf("%s\n", member_info[i][10]);
        printf("---------------------------------------------------------------------------------------------\n");
    }

    return 0;
}
