`dissent` is the variable that is visible on several pieces of UI, and represents the percentage of dissent in the nation.<br>
The variable is 1 to 1%, which means that adding for example, 25 to the variable will result in an addition of 25% to dissent.

However, `dissent` is merely the final calculation as completed in `common/scripted_effects/dpolitics_effects` in the `recalculate_dissent` function. This function should be called everytime you modify the `dissent_base` variable, which is the actual base value of dissent.

Creating modifiers for dissent can be slightly tedious, but it's necessary for it to work. When creating a modifier, you will typically use a `custom_modifier_tooltip` to display the rate of change for dissent. Dissent updates every week so be sure to make any localisation you create align with that fact. You can view existing tooltips in a language's tooltips localisation file. You will need to do the following to implement this in totality:

You can view the existing implementations of traits or ideas to get an idea of how to implement it, heres one:

```
if = {
	limit = {
		has_idea = reform_cl_total_individual_freedom
	}
	add_to_variable = { dissent_change_base = 0.1 }
}
```

Simply do a similar thing in order to implement your brand new weekly dissent modifier.

If you want one that simply flatly modifies the base dissent or by a percentage. You will have to do something a little different:

```
if = {
	limit = {
		has_idea = your_idea_goes_here
	}
	add_to_variable = { dissent_base = 0.1 } # By a constant number (in this case +10% constantly.)
}
```

```
if = {
	limit = {
		has_idea = your_idea_goes_here
	}
	multiply_variable = { dissent_base = 1.1 } # By a percentage (in this case +10% of the base dissent.)
}
```

Hopefully this guide has helped you understand how to implement new modifiers for dissent.