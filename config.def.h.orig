/* See LICENSE file for copyright and license details. */

/* appearance */
static const unsigned int borderpx  = 2;        /* border pixel of windows */
static const unsigned int gappx     = 16;        /* gap size between windows */
static const unsigned int snap      = 32;       /* snap pixel */
static const int showbar            = 1;        /* 0 means no bar */
static const int topbar             = 1;        /* 0 means bottom bar */
static const char *fonts[]          = { "Fira Mono:size=12" };
static const char dmenufont[]       = "Fira Mono:size=12";
// background color
static const char col_gray1[]       = "#282828";
// inactive window border color
static const char col_gray2[]       = "#928374";
// font color
static const char col_gray3[]       = "#d5c4a1";
// current tag and current window font color
static const char col_gray4[]       = "#fbf1c7";
// top bar second color and active window border color
static const char col_cyan[]        = "#d79921";
/* gruvbox colors */
static const char col_fg[]          = "#ebdbb2";
static const char col_bg[]          = "#282828";
static const char col_bg1[]         = "#3c3836";
static const char col_gray[]        = "#a89984";
static const char col_green[]       = "#98971a";
static const char col_aqua[]        = "#8ec07c";
static const char col_yellow[]      = "#d79921";

static const char *colors[][3]      = {
	/*               fg         bg         border   */
	[SchemeNorm] = { col_fg, col_bg, col_gray2 },
	[SchemeSel]  = { col_fg, col_yellow,  col_yellow  },
};

/* tagging */
static const char *tags[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };

static const Rule rules[] = {
	/* xprop(1):
	 *	WM_CLASS(STRING) = instance, class
	 *	WM_NAME(STRING) = title
	 */
	/* class      instance    title                     tags mask     isfloating   monitor */
	{ "Gimp",     NULL,       NULL,                     0,            1,           -1 },
	{ "Firefox",  NULL,       "Firefox Preferences",    0,            True,        -1 },
};

/* layout(s) */
static const float mfact     = 0.55; /* factor of master area size [0.05..0.95] */
static const int nmaster     = 1;    /* number of clients in master area */
static const int resizehints = 1;    /* 1 means respect size hints in tiled resizals */

static const Layout layouts[] = {
	/* symbol     arrange function */
	{ "[]=",      tile },    /* first entry is default */
	{ "[M]",      monocle },
 	{ "><>",      NULL },    /* no layout function means floating behavior */
  { NULL,       NULL },
};

/* key definitions */
#define MODKEY Mod4Mask
#define ALTKEY Mod1Mask
#define RALTKEY Mod3Mask
#define TAGKEYS(KEY,TAG) \
	{ MODKEY,                       KEY,      view,           {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask,           KEY,      toggleview,     {.ui = 1 << TAG} }, \
	{ MODKEY|ShiftMask,             KEY,      tag,            {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask|ShiftMask, KEY,      toggletag,      {.ui = 1 << TAG} }, \
        { ALTKEY|ControlMask,                       KEY,      focusnthmon,    {.i  = TAG } }, \
        { ALTKEY|ControlMask|ShiftMask,             KEY,      tagnthmon,      {.i  = TAG } },


/* helper for spawning shell commands in the pre dwm-5.0 fashion */
#define SHCMD(cmd) { .v = (const char*[]){ "/bin/sh", "-c", cmd, NULL } }

/* commands */
static char dmenumon[2] = "0"; /* component of dmenucmd, manipulated in spawn() */
static const char *dmenucmd[]     = { "dmenu_run", "-m", dmenumon, "-fn", dmenufont, "-nb", col_bg, "-nf", col_fg, "-sb", col_bg1, "-sf", col_yellow, NULL };
static const char *termcmd[]      = { "kitty", NULL };
static const char *browsercmd[]   = { "firefox", NULL };
static const char *voldown[]	    = { "pactl", "set-sink-volume", "@DEFAULT_SINK@", "-5%", NULL};
static const char *volup[]	      = { "pactl", "set-sink-volume", "@DEFAULT_SINK@", "+5%", NULL};
static const char *volmute[]	    = { "pactl", "set-sink-mute", "@DEFAULT_SINK@", "toggle", NULL};
static const char *passcmd[]      = { "passmenu", NULL };
static const char *mpvcmd[]       = { "mpvclip", NULL };
static const char *shutdowncmd[]  = { "shutdown", "-h", "now", NULL };

#include "patches/shift-tools.c"
#include "patches/push.c"
#include <X11/XF86keysym.h>
static Key keys[] = {
	/* modifier                     key        function        argument */
	{ MODKEY,                       XK_p,      spawn,          {.v = passcmd } },
  { ALTKEY,                       XK_space,  spawn,          {.v = dmenucmd } },
	{ MODKEY,                       XK_Return, spawn,          {.v = termcmd } },
  { MODKEY,                       XK_v,      spawn,          {.v = mpvcmd } },
  { MODKEY|ShiftMask,             XK_Escape, spawn,          {.v = shutdowncmd } },
  { MODKEY,                       XK_w,      spawn,          {.v = browsercmd } },
  { MODKEY,                       XK_c,      spawn,          SHCMD("codium") },
	{ MODKEY,                       XK_b,      togglebar,      {0} },
	{ ALTKEY,                       XK_Tab,    focusstack,     {.i = +1 } },
	{ ALTKEY|ShiftMask,             XK_Tab,    focusstack,     {.i = -1 } },
  { MODKEY,                       XK_j,      pushdown,       {0} },
  { MODKEY,                       XK_k,      pushup,         {0} },
	{ MODKEY,                       XK_i,      incnmaster,     {.i = +1 } },
	{ MODKEY,                       XK_d,      incnmaster,     {.i = -1 } },
	{ MODKEY,                       XK_h,      setmfact,       {.f = -0.05} },
	{ MODKEY,                       XK_l,      setmfact,       {.f = +0.05} },
	{ MODKEY|ShiftMask,             XK_Return, zoom,           {0} },
  { MODKEY,                       XK_Tab,    shiftview,      {.i = +1 } },
  { MODKEY|ShiftMask,             XK_Tab,    shiftview,      {.i = -1 } },
	{ MODKEY|ShiftMask,             XK_c,      killclient,     {0} },
  { ALTKEY,                       XK_F4,     killclient,     {0} },
	{ MODKEY,                       XK_t,      setlayout,      {.v = &layouts[0]} },
	{ MODKEY,                       XK_m,      setlayout,      {.v = &layouts[2]} },
	{ MODKEY,                       XK_space,  cyclelayout,    {.i = +1 } },
	{ MODKEY|ShiftMask,             XK_space,  togglefloating, {0} },
	{ MODKEY,                       XK_0,      view,           {.ui = ~0 } },
	{ MODKEY|ShiftMask,             XK_0,      tag,            {.ui = ~0 } },
	{ MODKEY,                       XK_comma,  focusmon,       {.i = -1 } },
	{ MODKEY,                       XK_period, focusmon,       {.i = +1 } },
	{ MODKEY|ShiftMask,             XK_comma,  tagmon,         {.i = -1 } },
	{ MODKEY|ShiftMask,             XK_period, tagmon,         {.i = +1 } },
	{ MODKEY,                       XK_minus,  setgaps,        {.i = -1 } },
	{ MODKEY,                       XK_equal,  setgaps,        {.i = +1 } },
	{ MODKEY|ShiftMask,             XK_equal,  setgaps,        {.i = 0  } },
	{ 0,                            XF86XK_AudioLowerVolume, spawn, {.v = voldown } },
	{ 0,                            XF86XK_AudioRaiseVolume, spawn, {.v = volup } },
	{ 0,                            XF86XK_AudioMute, spawn, {.v = volmute } },
  { 0,                            XF86XK_AudioPlay, spawn,   SHCMD("cplay") },
  { 0,                            XF86XK_AudioPrev, spawn,   SHCMD("cmus-remote --prev") },
  { 0,                            XF86XK_AudioNext, spawn,   SHCMD("cmus-remote --next") },
	TAGKEYS(                        XK_1,                      0)
	TAGKEYS(                        XK_2,                      1)
	TAGKEYS(                        XK_3,                      2)
	TAGKEYS(                        XK_4,                      3)
	TAGKEYS(                        XK_5,                      4)
	TAGKEYS(                        XK_6,                      5)
	TAGKEYS(                        XK_7,                      6)
	TAGKEYS(                        XK_8,                      7)
	TAGKEYS(                        XK_9,                      8)
	{ MODKEY|ShiftMask,             XK_q,      quit,           {0} },
};

/* button definitions */
/* click can be ClkTagBar, ClkLtSymbol, ClkStatusText, ClkWinTitle, ClkClientWin, or ClkRootWin */
static Button buttons[] = {
	/* click                event mask      button          function        argument */
	{ ClkLtSymbol,          0,              Button1,        setlayout,      {0} },
	{ ClkLtSymbol,          0,              Button3,        setlayout,      {.v = &layouts[2]} },
	{ ClkWinTitle,          0,              Button2,        zoom,           {0} },
	{ ClkStatusText,        0,              Button2,        spawn,          {.v = termcmd } },
	{ ClkClientWin,         MODKEY,         Button1,        movemouse,      {0} },
	{ ClkClientWin,         MODKEY,         Button2,        togglefloating, {0} },
	{ ClkClientWin,         MODKEY,         Button3,        resizemouse,    {0} },
	{ ClkTagBar,            0,              Button1,        view,           {0} },
	{ ClkTagBar,            0,              Button3,        toggleview,     {0} },
	{ ClkTagBar,            MODKEY,         Button1,        tag,            {0} },
	{ ClkTagBar,            MODKEY,         Button3,        toggletag,      {0} },
};

