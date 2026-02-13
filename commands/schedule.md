---
description: Find the best time for a meeting using AI-powered scheduling
argument-hint: [duration in minutes] [description]
disable-model-invocation: true
---

Help the user find optimal meeting times using `pear_find_best_time`.

1. Parse the arguments for duration (default 30 minutes if not specified) and any description
2. Use a search range of the next 5 business days unless the user specifies otherwise
3. Call `pear_find_best_time` with appropriate preferences (default to work hours 9-17, weekdays)
4. Present the top 3-5 results with:
   - Day and time
   - Score and reasoning
   - Any conflicts nearby
5. Ask the user which slot they want, then offer to create the event with `pear_create_event`

ARGUMENTS: $ARGUMENTS
