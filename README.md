
# How many frames per second will I get

I found a way to change the field of view and increase FPS by adjusting the parameters of shadows, decals, freezing some physical effects (for example, ragdolls and destruction of objects), reducing the number of fragments when destroying objects, reducing the maximum rendering distance for objects and disabling or reducing effects such as particles, HDR, SSAO, fog and others. If you want to make a video about this configuration, include me in the credits, it will help me a lot.

*__Don't expect a significant increase in FPS__, although I may be the first to give a significantly high FPS boost, I'm confident of performance gains, especially during team battles. I will update this post as new settings are discovered, so stay tuned!*

To use my settings, you need to open the file gameinfo.gi located in the folder with the game "steam\steamapps\common\Deadlock\game\citadel". When you find the file, you will see a line called "ConVars". Insert my code after the first parenthesis.

```cpp

ConVars
{
 
//---------------- GAMEINFO CONFIG — DYSON EDITION 2026 ---------------
// ------------------- Updated: 25.01.2026 | Optimized Build ----------

// ================ SYSTEM & THREADING (СИСТЕМА И ПОТОКИ) ================
// EN: Thread settings are moved up for priority
// RU: Настройки потоков вынесены вверх для приоритета
host_thread_mode "1"
r_threaded_particles "1"
r_threaded_renderables "1"
r_threaded_shadow_clip "1"
cl_threaded_bone_setup "1"
cl_threaded_client_leaf_system "1"
cl_threaded_bvs "1"
r_queued_post_processing "1"
engine_no_focus_sleep "0"
fps_max "0"

// ================ NETWORK (СЕТЬ) ================
cl_updaterate "128"
cl_cmdrate "128"
cl_interp "0.01"
cl_interp_ratio "1"
cl_maxpackets "256"
r_buffer_size "131072"
cl_predict "1"
cl_predictweapons "1"
cl_lagcompensation "1"
cl_smooth "0"
cl_smoothtime "0.01"
cl_resend "2"
cl_resendtimeout "2"
cl_resendinterval "2"
net_maxcleartime "0.005"
net_maxroutable "1200"
net_splitpacket_maxrate "30000"
cl_clock_buffer_ticks "1" // Сглаживание потери пакетов

// ================ GRAPHICS CORE (ГРАФИКА: ОСНОВА) ================
gpu_level "0"
cpu_level "0"
mat_set_shader_quality "0"
mat_queue_mode "2"
r_aspectratio "1.95" // 1.75=80fov | 2.15=90fov
// 2.4 = 100 fisheye effect (Jamside fov)
r_fastzreject "1"
r_norefresh "1"
r_dynamic "0"

// ================ SHADOWS & LIGHTING (ТЕНИ И СВЕТ) ================
r_shadows "0"
r_dynamic_shadows "0"
r_shadow_half_resolution "1"
r_shadowrendertotexture "0"
r_shadowmaxrendered "0"
r_shadowlod "0"
r_citadel_shadow_quality "0"
r_citadel_sun_shadow_slope_scale_depth_bias "1.0"
r_citadel_gpu_culling_shadows "1"
r_cull_duplicate_shadows "1"
r_cull_shadowcasters_using_bounds "1"
lb_enable_shadow_casting "0"
lb_csm_draw_alpha_tested "0"
lb_csm_draw_translucent "0"
lb_barnlight_shadowmap_scale "0.5"
lb_csm_cascade_size_override "1"
lb_dynamic_shadow_resolution_quantization "64"
lb_csm_override_staticgeo_cascades_value "0"
lb_csm_receiver_plane_depth_bias "0.00002"
lb_csm_receiver_plane_depth_bias_transmissive_backface "0.0002"
lb_sun_csm_size_cull_threshold_texels "30"
lb_dynamic_shadow_resolution_base "256"
sparseshadowtree_enable_rendering "1"

// Освещение (Lighting)
r_directlighting "0"
r_ssao "0"
r_ssao_strength "0"
r_citadel_ssao_bent_normals "false"
r_citadel_ssao_denoise_passes "0"
r_citadel_ssao_quality "0"
r_citadel_ssao_radius "0"
r_citadel_ssao_thin_occluder_compensation "0"
r_occlusion "1"
r_occlusion_culling "1"
r_light_static "0"
r_lightaverage "0"
r_worldlights "0"
r_worldlightmin "0.0001"
r_maxdlights "0"
r_hunkalloclightmaps "0"
r_lightmap_size_directional_irradiance "4"
mat_disable_lightwarp "1"
mat_disable_phong "1"
mat_disable_rimlight "1"

// ================ PARTICLES(ЧАСТИЦЫ: МЫЛО) ================

r_drawparticles "1" // Be sure to TURN it ON, otherwise you won't see any abilities! (Обязательно ВКЛ, иначе не видно скиллов)

// --- 1. ЛИМИТЫ (Чтоб консоль не орала) ---
// --- 1. LIMITS (So that the console doesn't spam errors) --- 
// RU: Ставим минимум, при котором движок не захлебывается ошибками 
// EN: We set the minimum at which the engine does not choke on errors.
cl_particle_max_count "1500" // 64 было слишком мало. 1500 хватит на замес 6x6. (64 was too little. 1500 is enough for 6x6 fight)
cl_particle_budget "0" // 0 = Динамический бюджет (убирает ошибки переполнения) (0 = Dynamic budget (removes overflow errors))
cl_particle_batch_mode "1" // Группировка частиц для снижения вызовов отрисовки (Grouping of particles to reduce rendering challenges)

// --- 2. КАЧЕСТВО (Убиваем графику в ноль) ---
// --- 2. QUALITY (Killing graphics to zero) ---
r_particle_low_res_render "1" // Рендерить частицы в низком разрешении (будут квадратными) (Render the particles in low resolution (they will be square))
r_particle_lighting_enable "0" // Отключить освещение частиц (плоский вид) (Turn off particle lighting (flat view))
r_particle_shadows "0" // Никаких теней от дыма/огня (No shadows from smoke/fire)
r_particle_cables_cast_shadows "0"
r_particle_max_detail_level "0" // Минимальная детализация (Minimum detail)
cl_particle_fallback_base "0" // Использовать базовые (дешевые) версии эффектов (Use basic (cheap) versions of effects)
cl_particle_fallback_multiplier "0" // Не размножать частицы (Do not multiply particles)


// --- 3. ОПТИМИЗАЦИЯ ВИДИМОСТИ ---
// --- 3. OPTIMIZE VISIBILITY ---
// Убираем то, что далеко или слишком мелкое (We remove what is far away or too shallow)
r_particle_max_size_cull "0" // 0 = НЕ удалять большие частицы (чтобы видеть ульты!) (0 = DO NOT remove large particles (to see the ults!))
r_particle_radius_cull "1" // Удалять мелкий мусор (Remove small debris)

// --- 4. УБИРАЕМ СПАМ КОНСОЛИ (СИНХРОНИЗАЦИЯ) ---
// --- 4. WE REMOVE SPAM FROM THE CONSOLE (SYNCHRONIZATION) ---
// RU: Эти команды вызывали ошибки предсказания, ставим дефолт или безопасные значения
// EN: These commands caused prediction errors, setting default or safe values.
r_particle_skip_update "0" // ВАЖНО: 0, иначе рассинхрон и лаги анимаций (IMPORTANT: 0, otherwise out of sync and animation lags)
r_particle_update_rate "0" // 0 = обновлять каждый тик (стабильно) (0 = update every tick (stable))
r_particle_timescale "1"
r_particle_sim_spike_threshold_ms "5" // Повысили порог, чтобы не спамило варнингами (Raised the threshold to avoid spamming with warnings)

// --- 5. МУСОР --- (5. GARBAGE)
r_RainParticleDensity "0" // Дождь выкл (Rain off)
particle_cluster_nodraw "1"
mat_reduceparticles "1" // Глобальная команда движка "уменьшить кол-во частиц" (Global engine command "reduce the number of particles")


// ================ MODELS, LOD & CULLING (МОДЕЛИ И ДАЛЬНОСТЬ) ================
r_rootlod "3" // Максимальное снижение качества моделей (Maximum reduction of model quality)
r_lod "3"
r_size_cull_threshold "1.6"
r_entity_cull_distance_multiplier "0.35"
r_cullforperformance "1"
r_gpu_cull "1"
r_gpu_cull_models "1"
r_gpu_cull_models_range "1200"
r_draw_batches "0"
r_model_lighting_simplified "1"
skeleton_instance_lod_optimization "1"
sv_ag2_low_skel_lod "true"
enable_boneflex "false"
r_flex "0"
r_eyes "0"
r_teeth "0"
r_eyegloss "0"
r_eyemove "0"
r_hair_ao "0"
cl_disable_ragdolls "1"
cl_ragdoll_limit "0" // Полное отключение рэгдоллов (Complete shutdown of ragdolls)
cl_ragdoll_fade_time "0"
cl_jiggle_bone_framerate_cutoff "0" // Отключить физику костей (Disable bone physics)

// ================ TEXTURES & STREAMING (ТЕКСТУРЫ) ================
r_texture_streaming "1"
r_texture_stream_pool_budget "256"
r_texture_stream_lowres_drop_rate "6"
r_texture_stream_mip_skip "1"
r_texture_stream_use_only_streamable "1"
r_texture_filter_textures "0"
r_texturefilteringquality "0"
r_texture_anisotropic "0" // Оставлено 0 (0 is normal)
mat_picmip "4" // Максимально мыльные текстуры для FPS (Maximally soapy textures for FPS)
mat_mip_linear "0"
mat_trilinear "0"
mat_forceaniso "0"
mat_reducefillrate "1"
mat_enable_uber_shaders "0"
mat_disable_fancy_blending "1"
r_render_view_scale "0.05" // Внимательно: это рендер в 5% разрешения (очень мыльно, но много FPS) (Carefully: this is a 5% resolution render (very soapy, but a lot of FPS))

// ================ PHYSICS, ROPES & DECALS (ФИЗИКА И МУСОР) ================
cl_phys_timescale "0" // Отключить физику (Disable physics)
cl_phys_sleep_enable "true"
cl_phys_props_max "0"
cl_phys_props_enable "0"
r_drawdecals "1"
r_decals "1"
r_queued_decals "0"
r_drawmodeldecals "0"
r_character_decal_resolution "1"
r_maxmodeldecal "0"
r_drawropes "0"
rope_collide "0"
rope_subdiv "0"
rope_wind_dist "0"
rope_smooth_enlarge "0"
rope_smooth_maxalpha "0"
rope_smooth_maxalphawidth "0"
rope_smooth_minalpha "0"
rope_smooth_minwidth "0"
r_ropetranslucent "0"
cloth_update "1"
cloth_sim_on_tick "0"

// ================ ATMOSPHERE & WATER (ВОДА И НЕБО) ================
r_drawskybox "0"
r_draw3dskybox "0"
r_monitor_3dskybox "0"
r_fog_enable "0"
r_enable_volume_fog "0"
r_enable_gradient_fog "0"
r_enable_cubemap_fog "0"
r_citadel_fog_quality "0"
r_waterforceexpensive "0"
r_drawwater "0"
r_cheapwaterstart "0"
r_cheapwaterend "1"
mat_disable_water "1"

// ================ POST-PROCESS & MISC (ПОСТОБРАБОТКА) ================
mat_postprocess_enable "0"
mat_hdr_level "0"
mat_tonemapping_occlusion_use_stencil "0"
mat_dynamic_tonemapping "0"
mat_auto_reduce_quality "1"
mat_auto_reduce_materials "1"
mat_disable_bloom "1"
mat_disable_bands "1"
mat_disable_software_led "1"
mat_disable_distortion "1"
mat_disable_fancy_alpha "1"
mat_force_bloom "0"
mat_force_tonemap "0"
mat_colcorrection_disableentities "0"
mat_colorcorrection "0"
mat_motion_blur_enabled "0"
r_citadel_motion_blur "0"
r_depth_of_field "0"
r_lensflare "0"
r_effects_bloom "0"
r_post_bloom "0"
r_screenoverlay "0"
r_filmgrain "0"
r_distancefield_enable "1"

// ================ ОТКЛЮЧЕНИЕ СВЕЧЕНИЯ КРИПОВ (TROOPERS) ================

citadel_trooper_glow_disabled "1" // 1 = Отключить свечение вражеских крипов (1 = Disable the glow of enemy creeps)
citadel_trooper_friendly_glow_disabled "1" // 1 = Отключить свечение своих крипов (1 = Turn off the glow of your creeps)
r_citadel_outlines "1" // Важно для геймплея (обводка врагов) (Important for gameplay (tracing enemies))
// RU: Дополнительно: убрать обводку через стены (X-Ray эффект)
// EN: Optional: remove the outline through the walls (X-Ray effect)
citadel_enemy_glow_enabled "0"


// ================ GAMEPLAY & UI (ГЕЙМПЛЕЙ И ИНТЕРФЕЙС) ================
r_drawtracers "1" // Трассеры включены (как просил в конце конфига) (Tracers are enabled (as requested at the end of the config))
r_drawtracers_firstperson "1"
cl_show_bloodspray "0"
cl_show_splashes "0"
cl_ejectbrass "0"
cl_playerspraydisable "1"
violence_hblood "0"
violence_ablood "0"
cl_burninggibs "0"
violence_hgibs "0"
violence_agibs "0"
citadel_damage_indicator "0"
citadel_damage_overlay "0"
citadel_damage_screen_effects "0"
citadel_post_damage_vignette "0"
citadel_show_new_damage_feedback_numbers "0"
citadel_hud_objective_health_enabled "2" // 0=Off, 1=Shrines, 2=T1/T2, 3=Barracks 0 = выключено, 1 = святилища, 2 = T1/T2, 3 = казармы
citadel_boss_glow_disabled "1"
citadel_hideout_ball_show_juggle_count "1"
citadel_hideout_ball_show_juggle_fx "1"
citadel_unit_status_use_new "false" // Чтобы вернуть старую полоску HP, поменяйте последнее слово true на false (To return the old HP strip, change the last word true to false.)
citadel_use_vertical_healthbars "0"
panorama_disable_box_shadow "1"
panorama_disable_blur "1"
panorama_disable_parallax "1"
panorama_disable_text_shadow "1"
panorama_disable_animations "1"
r_dashboard_render_quality "1"

// ================ AI & ENGINE (ИИ И ДВИЖОК) ================
ai_disabled "0"
ai_expression_optimization "1"
learning_rate "0.1"
think_limit "10"
engine_low_latency_sleep_after_client_tick "1"
engine_low_latency_sleep_after_render_tick "1"
battery_saver "0"
ik_final_fixup_enable "0"
ik_fabrik_align_chain "0"
phys_multithreading_enabled "1"
phys_show_stats "0"
phys_visualize_traces "0"
phys_log_updaters "0"
phys_dynamic_scaling "1"
snd_occlusion_debug "0"
snd_event_cone_debug "0"
snd_sound_areas_debug "0"
soundscape_radius_debug "0"
imgui_enable "0"
imgui_temp_enable "0"
imgui_debug_draw_dashboard_window "0"
imgui_enable_input "0"
r_light_flickering_enabled "1"
r_multiscattering "1"
r_lightmap_bicubic_filtering "1"
r_citadel_npr_outlines "0"
r_drawdevvisualizers "0"
r_debug_precipitation "0"
r_citadel_gpu_debug_draw "0"
r_flashlightvisualizetrace "0"
r_flashlightlockposition "0"
show_visibility_boxes "0"
g_debug_ragdoll_visualize "0"
modifier_aura_debug "0"
g_ragdoll_maxcount "0"
g_ragdoll_important_maxcount "0"
ragdoll_parallel_pose_control "0"
ragdoll_lru_debug_removal "0"
phys_powered_ragdoll_debug "0"
zipline_use_new_latch "0"
citadel_trooper_glow_disabled
citadel_trooper_friendly_glow_disabled

// ================ INPUT (ВВОД) ================
m_rawinput "1"
cl_input_enable_raw_keyboard "1"
m_filter "0"
input_virtualization_block_mouse "1"

// Очистка памяти (Clearing the memory)
r_pipeline_stats_present_flush "1"
r_pipeline_stats_command_flush "1"

// --------------- END OF CONFIG — DYSON EDITION 2026 ---

// THE REST OF THE ORIGINAL CONFIGURATION THAT YOU HAVE SHOULD BE HERE!

}
```
