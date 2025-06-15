# confederations_and_leagues
CK3 mod adding "Defensive Leagues" for non-Tribal/Nomadic realms through confederation system

TODO:
- Go through the files again and redo the tooltips/descriptions so that instead of have separate checks for which tooltip should be displayed (i.e. simply showing the word "League" instead of "Confederation"), instead, just try to overwrite the loc keys using customizable_localization, to hopefully maintain better compatibility.


"common\character_interactions\09_mpo_interactions.txt"
- [DONE, TEST] offer_confederation_interaction
- [DONE, TEST] join_confederation_interaction


"common\decisions\80_major_decisions.txt"
- found_kingdom_decision (if we allow kingdoms into confederations/leagues, can maybe modify this to allow confederation members to make new kingdoms)


"common\decisions\dlc_decisions\mpo\mpo_decisions.txt"
- [DONE, TEST] call_for_confederation_decision
- [DONE, TEST] leave_confederation_decision
- [DONE, TEST. DIDN'T DO CONFED-EMPIRE STUFF] confederation_kingdom_decision (and will need to look into either making a new decision that allows confederation empires to be made, or modify this one to instead give an empire title, if we allow kingdoms into confederations)


"common\factions\00_factions.txt"
- independence_faction (can_character_create_ui/can_character_create/can_character_join blocks seem to prevent this faction for Nomads/Tribes if liege is in a confederation. Need to look into this, whether to just leave the Nomad/Tribe limitation, extend it to "Leagues", or whatever)


"common\important_actions\09_mpo_actions.txt"
- action_offer_confederation (This is just one of the "important action" banners that appears at the top of the screen if the game realizes there is someone that will accept joining a confederation. Not a high priority, but can maybe see if there is a way to have the localization properly reflect the "Confederation"/"League" split)


"common\laws\00_realm_laws.txt"
- [DONE, TEST] crown_authority (The base game limits what tribal/nomadic_authority a confederation member can have. Will probably need to do that for crown_authority too for "League" members)


"common\laws\01_title_succession_laws.txt"
- confederation_elective_succession_law (I don't think I will need to change this, but figured I'd just note it down here in case I run into issues when implementing the faith-based confederations/leagues)


"common\lifestyle_perks\00_diplomacy_2_majesty_tree_perks.txt"
- [DONE, TEST. Only used as a modifier in offer_confederation_interaction] true_ruler_perk (The effect block shows that Tribes/Nomads, when offering to another ruler to join a confederation, have an increased chance for them to accept. I don't think this should be changed, as it could allow Tribes/Nomads a better fighting chance against the Feudal/Republic/etc realms that typically cover the map after converting from Imperator. Figured I'd mention this here just so it is known, in case it is decided that this should be extended to Feudal/Republics/etc for joining "Leagues")


"common\messages\01_alliance_messages.txt"
- msg_broken_confederation/msg_joined_confederation (While this file itself might not need to be changed, might need to look into changing their relevant loc keys found in "localization\english\dlc\mpo\mpo_interactions_l_english.yml" to better reflect the "Confederation"/"League" split. Not a high priority)


"common\on_action\confederation_on_actions.txt"
- This whole file might need to be modified to better fit the "Confederation"/"League" split, but will need to check each on_action in it to better determine what needs to be changed.


"common\on_action\game_start.txt"
- [DONE, TEST] Lines 1652-1661. This isn't super important since the converter doesn't map any Imperator tag to `k_magyar` and it properly checks if the title currently has a holder at game start, but just in case, could probably remove this section from the file, since it gives the special Confederation Elective succession law to `k_magyar`.


"common\on_action\title_on_actions.txt"
- [DONE, TEST] on_title_gain (Lines 452-460 makes someone leave a confederation they are in if they gain a kingdom+ title, so that will need to be modified based off how we determine to handle kingdoms in confederations/leagues)


"common\on_action\dlc\mpo\mpo_on_actions_2.txt"
- [DONE, TEST] on_government_change (Lines 589-600 makes it so that when you change government and are part of a confederation, if you are no longer Tribal/Nomadic, you are removed from the confederation. Will probably need to modify this so that you only leave the confederation/league if your new government isn't compatible with the confederation/league, i.e. if you are in a "League" and become Tribal, you should leave, but if you somehow become a Republic, you can stay)


"common\script_values\00_interaction_values.txt"
- duchy_confederation_vassals_value/duchy_confederation_vassals_value_recipient (Need to see exactly what these do, but it seems like it might give a negative opinion penalty to your vassals if you are in a confederation. Whatever it is seems like it might affect only Dukes, so might need to set up the Kingdom equivalent)


"common\script_values\02_religion_values.txt"
- holy_site_reform_tracker_value (I think this is what tracks the number of Holy Sites you own for reforming unreformed faiths. This counts Holy Sites in the realms of confederation members as being owned, making it a little easier to reform faiths. Should this be limited to just the Nomad/Tribal "Confederations", or should the "Leagues" be allowed to use this as well?)


"common\scripted_effects\09_dlc_mpo_scripted_effects.txt"
- [DONE, TEST] offer_confederation_accepter_effect (This shows the effect tooltips about what happens when creating/joining a confederation. Not a high priority, but this could be modified to better represent the "Confederation"/"League" split localization-wise)
- confederation_realm_transfer_effect (Not sure exactly what this is supposed to be used for, as it doesn't seem to be used anywhere)


"common\scripted_modifiers\00_elective_successions_scripted_modifiers.txt"
- [DONE, TEST] elector_voting_pattern_confederation_modifier (Need to check exactly what this is used for, but I think it affects who electors vote for in the Confederation Elective succession law. It has a part referencing the "confederation culture", so will likely at least need to modify it so that it also accounts for the "confederation faith", if I add that. Another part also makes a character more likely to be elected if they have higher prowess, could maybe also add in a part that takes something like learning/piety into consideration for faith-based confederation/leagues)


"common\scripted_modifiers\00_faction_modifiers.txt"
- independence_faction_create_blockers (Has a part that seems to make independence factions less likely/impossible for Nomads/Tribals if their primary title has the Confederation Elective succession law. Need to determine whether this should be extended to other governments in "Leagues", or just Tribes/Nomads in "Confederations")
- nation_fracturing_faction_blockers (Has a part that seems to make dissolution factions less likely/impossible for Nomads/Tribals if their primary title has the Confederation Elective succession law. Need to determine whether this should be extended to other governments in "Leagues", or just Tribes/Nomads in "Confederations")


"common\scripted_triggers\00_religious_triggers.txt"
- num_realm_holy_sites_faithful_holders (Deals with counting number of held holy sites, like with holy_site_reform_tracker_value, need to determine whether this should be changed to allow only Tribe/Nomadic "Confederations", or "Leagues" too)


"common\scripted_triggers\mpo_scripted_triggers.txt"
- [DONE, TEST] valid_confederation_member_trigger (Determines whether a character can actually join a confederation. Will need to change to account for things like the "Confederation"/"League" split, and kingdoms being allowed if we decide to)
- confedration_foe_sub_trigger/confederation_foe_trigger/confederation_neighboring_foe_trigger (Used to determine whether there is a valid strong "foe" nearby that is worth confederating against. Not sure if these will need to be changed, but wanted to mention it here just in case so they're listed)


"common\succession_election\09_confederation_elective.txt"
- [DONE, TEST] This is the definition of the Confederation Elective succession law, so will likely need to modify this to account for faith-based confederations/leagues, kingdoms if we allow them in, and maybe some changes focused around the "Confederation"/"League" split.


"events\decisions_events\mpo_greatest_of_khans_events.txt"
- [DONE, TEST] mpo_greatest_of_khans.0002/mpo_greatest_of_khans_0002_confederation_trigger (These deal with the event for when someone else becomes the Greatest of Khans, and the trigger checks if there is a valid confederation nearby for you to join against the new Khan. Will likely need to modify this so that the trigger properly checks if the character has the proper government to join the neighboring "Confederation"/"League")
- [DONE, TEST] mpo_greatest_of_khans.0003/mpo_greatest_of_khans.1001 (Also checks valid confederations, whether characters can join, etc. Uses the above trigger, so need to see if this even needs further modification after that trigger is changed)


"events\dlc\mpo\mpo_decisions_events.txt"
- [DONE, TEST] mpo_decisions_events.0001 (Event triggered when you decide to try forming a confederation. Will at least need to change it to account for "Confederation"/"League" split)
- [DONE, TEST] mpo_decisions_events.0002/mpo_decisions_events.0003 (Event triggered for you and your old confederation members, respectively, when you decide to leave your confederation, need to account for "Confederation"/"League" split)
- [NO CHANGES NEEDED] mpo_decisions_events.0004/mpo_decisions_events.0005 (Event triggered when a confederation is elevated to a kingdom for the new vassals and king, respectively. Need to account for "Confederation"/"League" split, and maybe for if we decide to allow kingdoms into confederations, we will need to handle empire-confederation titles too)


"events\dlc\mpo\mpo_interactions_events.txt"
- [DONE, TEST] mpo_interactions_events.0001 (Seems to be triggered after someone uses the Join Confederation interaction, and handles creating the confederation, if it doesn't exist, or adding the new member to it. Will need to account for "Confederation"/"League" split, new faith-based confederations/leagues, and however we decide to handle naming.)
- [DONE, TEST] mpo_interactions_events.0002 (Seems to be triggered after joining/creating a confederation, and handles setting up some of the effects, like the fertility bonus for Nomads. Need to modify to account for "Confederation"/"League" split, maybe faith-based confederations/leagues if they end up getting anything special)
- [DONE, TEST] mpo_interactions_events.0003/mpo_interactions_events.0004 (Handles the event sent back when you ask another character to join a confederation for if they accept or decline, respectively. Might need to modify for "Confederation"/"League" split.)
- [NO CHANGES NEEDED] mpo_interactions_events.0030 (Same as above, but seems to be used if you ask someone else to join their confederation)


There is also a lot of loc keys that revolve around confederations, but those can probably be looked at as their relevant game content gets changed (like a decision's description)
