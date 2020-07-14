---
title: tmux
layout: post
---

<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  
  <!--<link rel="stylesheet" href="./css/mandoc.css" type="text/css" media="all">-->
  <title>tmux(1) - OpenBSD manual pages</title>
</head>
<body>

<table class="head">
  <tbody><tr>
    <td class="head-ltitle">TMUX(1)</td>
    <td class="head-vol">General Commands Manual</td>
    <td class="head-rtitle">TMUX(1)</td>
  </tr>
</tbody></table>
<div class="manual-text">
<h1 class="Sh" title="Sh" id="NAME"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#NAME">NAME</a></h1>
<b class="Nm" title="Nm">tmux</b> — <span class="Nd" title="Nd">terminal
  multiplexer</span>
<h1 class="Sh" title="Sh" id="SYNOPSIS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#SYNOPSIS">SYNOPSIS</a></h1>
<table class="Nm">
  <tbody><tr>
    <td><b class="Nm" title="Nm">tmux</b></td>
    <td>[<span class="Op"><b class="Fl" title="Fl">-2Cluv</b></span>]
      [<span class="Op"><b class="Fl" title="Fl">-c</b>&nbsp;<var class="Ar" title="Ar">shell-command</var></span>]
      [<span class="Op"><b class="Fl" title="Fl">-f</b>&nbsp;<var class="Ar" title="Ar">file</var></span>]
      [<span class="Op"><b class="Fl" title="Fl">-L</b>&nbsp;<var class="Ar" title="Ar">socket-name</var></span>]
      [<span class="Op"><b class="Fl" title="Fl">-S</b>&nbsp;<var class="Ar" title="Ar">socket-path</var></span>]
      [<span class="Op"><var class="Ar" title="Ar">command</var>&nbsp;[<span class="Op"><var class="Ar" title="Ar">flags</var></span>]</span>]</td>
  </tr>
</tbody></table>
<h1 class="Sh" title="Sh" id="DESCRIPTION"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#DESCRIPTION">DESCRIPTION</a></h1>
<b class="Nm" title="Nm">tmux</b> is a terminal multiplexer: it enables a number
  of terminals to be created, accessed, and controlled from a single screen.
  <b class="Nm" title="Nm">tmux</b> may be detached from a screen and continue
  running in the background, then later reattached.
<div class="Pp"></div>
When <b class="Nm" title="Nm">tmux</b> is started it creates a new
  <i class="Em" title="Em">session</i> with a single
  <i class="Em" title="Em">window</i> and displays it on screen. A status line
  at the bottom of the screen shows information on the current session and is
  used to enter interactive commands.
<div class="Pp"></div>
A session is a single collection of <i class="Em" title="Em">pseudo
  terminals</i> under the management of <b class="Nm" title="Nm">tmux</b>. Each
  session has one or more windows linked to it. A window occupies the entire
  screen and may be split into rectangular panes, each of which is a separate
  pseudo terminal (the <a class="Xr" title="Xr" href="http://man.openbsd.org/pty.4">pty(4)</a> manual
  page documents the technical details of pseudo terminals). Any number of
  <b class="Nm" title="Nm">tmux</b> instances may connect to the same session,
  and any number of windows may be present in the same session. Once all
  sessions are killed, <b class="Nm" title="Nm">tmux</b> exits.
<div class="Pp"></div>
Each session is persistent and will survive accidental disconnection (such as
  <a class="Xr" title="Xr" href="http://man.openbsd.org/ssh.1">ssh(1)</a> connection timeout) or
  intentional detaching (with the ‘<code class="Li">C-b d</code>’
  key strokes). <b class="Nm" title="Nm">tmux</b> may be reattached using:
<div class="Pp"></div>
<div class="D1"><code class="Li">$ tmux attach</code></div>
<div class="Pp"></div>
In <b class="Nm" title="Nm">tmux</b>, a session is displayed on screen by a
  <i class="Em" title="Em">client</i> and all sessions are managed by a single
  <i class="Em" title="Em">server</i>. The server and each client are separate
  processes which communicate through a socket in
  <i class="Pa" title="Pa">/tmp</i>.
<div class="Pp"></div>
The options are as follows:
<dl class="Bl-tag" style="margin-left: 17.40ex;">
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#2"><b class="Fl" title="Fl" id="2">-2</b></a></dt>
  <dd class="It-tag">Force <b class="Nm" title="Nm">tmux</b> to assume the
      terminal supports 256 colours.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#C"><b class="Fl" title="Fl" id="C">-C</b></a></dt>
  <dd class="It-tag">Start in control mode (see the
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#CONTROL_MODE">CONTROL MODE</a> section).
      Given twice (<b class="Fl" title="Fl">-CC</b>) disables echo.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#c"><b class="Fl" title="Fl" id="c">-c</b></a>
    <var class="Ar" title="Ar">shell-command</var></dt>
  <dd class="It-tag">Execute <var class="Ar" title="Ar">shell-command</var>
      using the default shell. If necessary, the
      <b class="Nm" title="Nm">tmux</b> server will be started to retrieve the
      <b class="Ic" title="Ic">default-shell</b> option. This option is for
      compatibility with <a class="Xr" title="Xr" href="http://man.openbsd.org/sh.1">sh(1)</a> when
      <b class="Nm" title="Nm">tmux</b> is used as a login shell.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#f"><b class="Fl" title="Fl" id="f">-f</b></a>
    <var class="Ar" title="Ar">file</var></dt>
  <dd class="It-tag">Specify an alternative configuration file. By default,
      <b class="Nm" title="Nm">tmux</b> loads the system configuration file from
      <i class="Pa" title="Pa">/etc/tmux.conf</i>, if present, then looks for a
      user configuration file at <i class="Pa" title="Pa">~/.tmux.conf</i>.
    <div class="Pp"></div>
    The configuration file is a set of <b class="Nm" title="Nm">tmux</b>
      commands which are executed in sequence when the server is first started.
      <b class="Nm" title="Nm">tmux</b> loads configuration files once when the
      server process has started. The <b class="Ic" title="Ic">source-file</b>
      command may be used to load a file later.
    <div class="Pp"></div>
    <b class="Nm" title="Nm">tmux</b> shows any error messages from commands in
      configuration files in the first session created, and continues to process
      the rest of the configuration file.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#L"><b class="Fl" title="Fl" id="L">-L</b></a>
    <var class="Ar" title="Ar">socket-name</var></dt>
  <dd class="It-tag"><b class="Nm" title="Nm">tmux</b> stores the server socket
      in a directory under <code class="Ev" title="Ev">TMUX_TMPDIR</code> or
      <i class="Pa" title="Pa">/tmp</i> if it is unset. The default socket is
      named <i class="Em" title="Em">default</i>. This option allows a different
      socket name to be specified, allowing several independent
      <b class="Nm" title="Nm">tmux</b> servers to be run. Unlike
      <b class="Fl" title="Fl">-S</b> a full path is not necessary: the sockets
      are all created in the same directory.
    <div class="Pp"></div>
    If the socket is accidentally removed, the
      <code class="Dv" title="Dv">SIGUSR1</code> signal may be sent to the
      <b class="Nm" title="Nm">tmux</b> server process to recreate it (note that
      this will fail if any parent directories are missing).</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#l"><b class="Fl" title="Fl" id="l">-l</b></a></dt>
  <dd class="It-tag">Behave as a login shell. This flag currently has no effect
      and is for compatibility with other shells when using tmux as a login
      shell.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#S"><b class="Fl" title="Fl" id="S">-S</b></a>
    <var class="Ar" title="Ar">socket-path</var></dt>
  <dd class="It-tag">Specify a full alternative path to the server socket. If
      <b class="Fl" title="Fl">-S</b> is specified, the default socket directory
      is not used and any <b class="Fl" title="Fl">-L</b> flag is ignored.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#u"><b class="Fl" title="Fl" id="u">-u</b></a></dt>
  <dd class="It-tag">When starting, <b class="Nm" title="Nm">tmux</b> looks for
      the <code class="Ev" title="Ev">LC_ALL</code>,
      <code class="Ev" title="Ev">LC_CTYPE</code> and
      <code class="Ev" title="Ev">LANG</code> environment variables: if the
      first found contains ‘<code class="Li">UTF-8</code>’, then
      the terminal is assumed to support UTF-8. This is not always correct: the
      <b class="Fl" title="Fl">-u</b> flag explicitly informs
      <b class="Nm" title="Nm">tmux</b> that UTF-8 is supported.
    <div class="Pp"></div>
    Note that <b class="Nm" title="Nm">tmux</b> itself always accepts UTF-8;
      this controls whether it will send UTF-8 characters to the terminal it is
      running (if not, they are replaced by
      ‘<code class="Li">_</code>’).</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#v"><b class="Fl" title="Fl" id="v">-v</b></a></dt>
  <dd class="It-tag">Request verbose logging. Log messages will be saved into
      <i class="Pa" title="Pa">tmux-client-PID.log</i> and
      <i class="Pa" title="Pa">tmux-server-PID.log</i> files in the current
      directory, where <i class="Em" title="Em">PID</i> is the PID of the server
      or client process.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-v</b> is specified twice, an additional
      <i class="Pa" title="Pa">tmux-out-PID.log</i> file is generated with a
      copy of everything <b class="Nm" title="Nm">tmux</b> writes to the
      terminal.
    <div class="Pp"></div>
    The <code class="Dv" title="Dv">SIGUSR2</code> signal may be sent to the
      <b class="Nm" title="Nm">tmux</b> server process to toggle logging between
      on (as if <b class="Fl" title="Fl">-v</b> was given) and off.</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -17.40ex;"><var class="Ar" title="Ar">command</var>
    [<span class="Op"><var class="Ar" title="Ar">flags</var></span>]</dt>
  <dd class="It-tag">This specifies one of a set of commands used to control
      <b class="Nm" title="Nm">tmux</b>, as described in the following sections.
      If no commands are specified, the <b class="Ic" title="Ic">new-session</b>
      command is assumed.</dd>
</dl>
<h1 class="Sh" title="Sh" id="KEY_BINDINGS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#KEY_BINDINGS">KEY
  BINDINGS</a></h1>
<b class="Nm" title="Nm">tmux</b> may be controlled from an attached client by
  using a key combination of a prefix key,
  ‘<code class="Li">C-b</code>’ (Ctrl-b) by default, followed by a
  command key.
<div class="Pp"></div>
The default command key bindings are:
<div class="Pp"></div>
<div class="Bl-tag" style="margin-left: 6.00ex;">
<dl class="Bl-tag Bl-compact" style="margin-left: 15.00ex;">
  <dt class="It-tag" style="margin-left: -15.00ex;">C-b</dt>
  <dd class="It-tag">Send the prefix key (C-b) through to the application.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">C-o</dt>
  <dd class="It-tag">Rotate the panes in the current window forwards.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">C-z</dt>
  <dd class="It-tag">Suspend the <b class="Nm" title="Nm">tmux</b> client.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">!</dt>
  <dd class="It-tag">Break the current pane out of the window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">"</dt>
  <dd class="It-tag">Split the current pane into two, top and bottom.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">#</dt>
  <dd class="It-tag">List all paste buffers.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">$</dt>
  <dd class="It-tag">Rename the current session.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">%</dt>
  <dd class="It-tag">Split the current pane into two, left and right.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">&amp;</dt>
  <dd class="It-tag">Kill the current window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">'</dt>
  <dd class="It-tag">Prompt for a window index to select.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">(</dt>
  <dd class="It-tag">Switch the attached client to the previous session.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">)</dt>
  <dd class="It-tag">Switch the attached client to the next session.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">,</dt>
  <dd class="It-tag">Rename the current window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">-</dt>
  <dd class="It-tag">Delete the most recently copied buffer of text.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">.</dt>
  <dd class="It-tag">Prompt for an index to move the current window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">0 to 9</dt>
  <dd class="It-tag">Select windows 0 to 9.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">:</dt>
  <dd class="It-tag">Enter the <b class="Nm" title="Nm">tmux</b> command
    prompt.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">;</dt>
  <dd class="It-tag">Move to the previously active pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">=</dt>
  <dd class="It-tag">Choose which buffer to paste interactively from a
    list.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">?</dt>
  <dd class="It-tag">List all key bindings.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">D</dt>
  <dd class="It-tag">Choose a client to detach.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">L</dt>
  <dd class="It-tag">Switch the attached client back to the last session.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">[</dt>
  <dd class="It-tag">Enter copy mode to copy text or view the history.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">]</dt>
  <dd class="It-tag">Paste the most recently copied buffer of text.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">c</dt>
  <dd class="It-tag">Create a new window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">d</dt>
  <dd class="It-tag">Detach the current client.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">f</dt>
  <dd class="It-tag">Prompt to search for text in open windows.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">i</dt>
  <dd class="It-tag">Display some information about the current window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">l</dt>
  <dd class="It-tag">Move to the previously selected window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">n</dt>
  <dd class="It-tag">Change to the next window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">o</dt>
  <dd class="It-tag">Select the next pane in the current window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">p</dt>
  <dd class="It-tag">Change to the previous window.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">q</dt>
  <dd class="It-tag">Briefly display pane indexes.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">r</dt>
  <dd class="It-tag">Force redraw of the attached client.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">m</dt>
  <dd class="It-tag">Mark the current pane (see
      <b class="Ic" title="Ic">select-pane</b>
    <b class="Fl" title="Fl">-m</b>).</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M</dt>
  <dd class="It-tag">Clear the marked pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">s</dt>
  <dd class="It-tag">Select a new session for the attached client
    interactively.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">t</dt>
  <dd class="It-tag">Show the time.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">w</dt>
  <dd class="It-tag">Choose the current window interactively.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">x</dt>
  <dd class="It-tag">Kill the current pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">z</dt>
  <dd class="It-tag">Toggle zoom state of the current pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">{</dt>
  <dd class="It-tag">Swap the current pane with the previous pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">}</dt>
  <dd class="It-tag">Swap the current pane with the next pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">~</dt>
  <dd class="It-tag">Show previous messages from
      <b class="Nm" title="Nm">tmux</b>, if any.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">Page Up</dt>
  <dd class="It-tag">Enter copy mode and scroll one page up.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">Up, Down</dt>
  <dd class="It-tag" style="width: auto;">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">Left, Right</dt>
  <dd class="It-tag">Change to the pane above, below, to the left, or to the
      right of the current pane.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-1 to M-5</dt>
  <dd class="It-tag">Arrange panes in one of the five preset layouts:
      even-horizontal, even-vertical, main-horizontal, main-vertical, or
    tiled.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">Space</dt>
  <dd class="It-tag">Arrange the current window in the next preset layout.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-n</dt>
  <dd class="It-tag">Move to the next window with a bell or activity
    marker.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-o</dt>
  <dd class="It-tag">Rotate the panes in the current window backwards.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-p</dt>
  <dd class="It-tag">Move to the previous window with a bell or activity
    marker.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">C-Up, C-Down</dt>
  <dd class="It-tag" style="width: auto;">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">C-Left, C-Right</dt>
  <dd class="It-tag">Resize the current pane in steps of one cell.</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-Up, M-Down</dt>
  <dd class="It-tag" style="width: auto;">&nbsp;</dd>
  <dt class="It-tag" style="margin-left: -15.00ex;">M-Left, M-Right</dt>
  <dd class="It-tag">Resize the current pane in steps of five cells.</dd>
</dl>
</div>
<div class="Pp"></div>
Key bindings may be changed with the <b class="Ic" title="Ic">bind-key</b> and
  <b class="Ic" title="Ic">unbind-key</b> commands.
<h1 class="Sh" title="Sh" id="COMMANDS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#COMMANDS">COMMANDS</a></h1>
This section contains a list of the commands supported by
  <b class="Nm" title="Nm">tmux</b>. Most commands accept the optional
  <b class="Fl" title="Fl">-t</b> (and sometimes
  <b class="Fl" title="Fl">-s</b>) argument with one of
  <var class="Ar" title="Ar">target-client</var>,
  <var class="Ar" title="Ar">target-session</var>
  <var class="Ar" title="Ar">target-window</var>, or
  <var class="Ar" title="Ar">target-pane</var>. These specify the client,
  session, window or pane which a command should affect.
<div class="Pp"></div>
<var class="Ar" title="Ar">target-client</var> should be the name of the client,
  typically the <a class="Xr" title="Xr" href="http://man.openbsd.org/pty.4">pty(4)</a> file to which
  the client is connected, for example either of
  <i class="Pa" title="Pa">/dev/ttyp1</i> or <i class="Pa" title="Pa">ttyp1</i>
  for the client attached to <i class="Pa" title="Pa">/dev/ttyp1</i>. If no
  client is specified, <b class="Nm" title="Nm">tmux</b> attempts to work out
  the client currently in use; if that fails, an error is reported. Clients may
  be listed with the <b class="Ic" title="Ic">list-clients</b> command.
<div class="Pp"></div>
<var class="Ar" title="Ar">target-session</var> is tried as, in order:
<ol class="Bl-enum" style="margin-left: 6.00ex;">
  <li class="It-enum">A session ID prefixed with a $.</li>
  <li class="It-enum">An exact name of a session (as listed by the
      <b class="Ic" title="Ic">list-sessions</b> command).</li>
  <li class="It-enum">The start of a session name, for example
      ‘<code class="Li">mysess</code>’ would match a session named
      ‘<code class="Li">mysession</code>’.</li>
  <li class="It-enum">An
      <a class="Xr" title="Xr" href="http://man.openbsd.org/fnmatch.3">fnmatch(3)</a> pattern which is
      matched against the session name.</li>
</ol>
<div class="Pp"></div>
If the session name is prefixed with an
  ‘<code class="Li">=</code>’, only an exact match is accepted (so
  ‘<code class="Li">=mysess</code>’ will only match exactly
  ‘<code class="Li">mysess</code>’, not
  ‘<code class="Li">mysession</code>’).
<div class="Pp"></div>
If a single session is found, it is used as the target session; multiple matches
  produce an error. If a session is omitted, the current session is used if
  available; if no current session is available, the most recently used is
  chosen.
<div class="Pp"></div>
<var class="Ar" title="Ar">target-window</var> (or
  <var class="Ar" title="Ar">src-window</var> or
  <var class="Ar" title="Ar">dst-window</var>) specifies a window in the form
  <i class="Em" title="Em">session</i>:<i class="Em" title="Em">window</i>.
  <i class="Em" title="Em">session</i> follows the same rules as for
  <var class="Ar" title="Ar">target-session</var>, and
  <i class="Em" title="Em">window</i> is looked for in order as:
<ol class="Bl-enum" style="margin-left: 6.00ex;">
  <li class="It-enum">A special token, listed below.</li>
  <li class="It-enum">A window index, for example
      ‘<code class="Li">mysession:1</code>’ is window 1 in session
      ‘<code class="Li">mysession</code>’.</li>
  <li class="It-enum">A window ID, such as @1.</li>
  <li class="It-enum">An exact window name, such as
      ‘<code class="Li">mysession:mywindow</code>’.</li>
  <li class="It-enum">The start of a window name, such as
      ‘<code class="Li">mysession:mywin</code>’.</li>
  <li class="It-enum">As an
      <a class="Xr" title="Xr" href="http://man.openbsd.org/fnmatch.3">fnmatch(3)</a> pattern matched
      against the window name.</li>
</ol>
<div class="Pp"></div>
Like sessions, a ‘<code class="Li">=</code>’ prefix will do an
  exact match only. An empty window name specifies the next unused index if
  appropriate (for example the <b class="Ic" title="Ic">new-window</b> and
  <b class="Ic" title="Ic">link-window</b> commands) otherwise the current
  window in <i class="Em" title="Em">session</i> is chosen.
<div class="Pp"></div>
The following special tokens are available to indicate particular windows. Each
  has a single-character alternative form.
<table class="Bl-column">
  <colgroup>
    <col style="width: 15.00ex;">
    <col style="min-width: 1.00ex;">
  </colgroup>
  <tbody><tr class="It-column">
    <td class="It-column"><b class="Sy" title="Sy">Token</b></td>
    <td class="It-column"><b class="Sy" title="Sy"></b></td>
    <td class="It-column"><b class="Sy" title="Sy">Meaning</b></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{start}"><code class="Li" id="{start}">{start}</code></a></td>
    <td class="It-column">^</td>
    <td class="It-column">The lowest-numbered window</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{end}"><code class="Li" id="{end}">{end}</code></a></td>
    <td class="It-column">$</td>
    <td class="It-column">The highest-numbered window</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{last}"><code class="Li" id="{last}">{last}</code></a></td>
    <td class="It-column">!</td>
    <td class="It-column">The last (previously current) window</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{next}"><code class="Li" id="{next}">{next}</code></a></td>
    <td class="It-column">+</td>
    <td class="It-column">The next window by number</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{previous}"><code class="Li" id="{previous}">{previous}</code></a></td>
    <td class="It-column">-</td>
    <td class="It-column">The previous window by number</td>
  </tr>
</tbody></table>
<div class="Pp"></div>
<var class="Ar" title="Ar">target-pane</var> (or
  <var class="Ar" title="Ar">src-pane</var> or
  <var class="Ar" title="Ar">dst-pane</var>) may be a pane ID or takes a similar
  form to <var class="Ar" title="Ar">target-window</var> but with the optional
  addition of a period followed by a pane index or pane ID, for example:
  ‘<code class="Li">mysession:mywindow.1</code>’. If the pane
  index is omitted, the currently active pane in the specified window is used.
  The following special tokens are available for the pane index:
<table class="Bl-column">
  <colgroup>
    <col style="width: 19.80ex;">
    <col style="min-width: 1.00ex;">
  </colgroup>
  <tbody><tr class="It-column">
    <td class="It-column"><b class="Sy" title="Sy">Token</b></td>
    <td class="It-column"><b class="Sy" title="Sy"></b></td>
    <td class="It-column"><b class="Sy" title="Sy">Meaning</b></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{last}"><code class="Li" id="{last}">{last}</code></a></td>
    <td class="It-column">!</td>
    <td class="It-column">The last (previously active) pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{next}"><code class="Li" id="{next}">{next}</code></a></td>
    <td class="It-column">+</td>
    <td class="It-column">The next pane by number</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{previous}"><code class="Li" id="{previous}">{previous}</code></a></td>
    <td class="It-column">-</td>
    <td class="It-column">The previous pane by number</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{top}"><code class="Li" id="{top}">{top}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The top pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{bottom}"><code class="Li" id="{bottom}">{bottom}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The bottom pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{left}"><code class="Li" id="{left}">{left}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The leftmost pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{right}"><code class="Li" id="{right}">{right}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The rightmost pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{top-left}"><code class="Li" id="{top-left}">{top-left}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The top-left pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{top-right}"><code class="Li" id="{top-right}">{top-right}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The top-right pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{bottom-left}"><code class="Li" id="{bottom-left}">{bottom-left}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The bottom-left pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{bottom-right}"><code class="Li" id="{bottom-right}">{bottom-right}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The bottom-right pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{up-of}"><code class="Li" id="{up-of}">{up-of}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The pane above the active pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{down-of}"><code class="Li" id="{down-of}">{down-of}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The pane below the active pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{left-of}"><code class="Li" id="{left-of}">{left-of}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The pane to the left of the active pane</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#{right-of}"><code class="Li" id="{right-of}">{right-of}</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">The pane to the right of the active pane</td>
  </tr>
</tbody></table>
<div class="Pp"></div>
The tokens ‘<code class="Li">+</code>’ and
  ‘<code class="Li">-</code>’ may be followed by an offset, for
  example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">select-window -t:+2
</pre>
</div>
<div class="Pp"></div>
In addition, <i class="Em" title="Em">target-session</i>,
  <i class="Em" title="Em">target-window</i> or
  <i class="Em" title="Em">target-pane</i> may consist entirely of the token
  ‘<code class="Li">{mouse}</code>’ (alternative form
  ‘<code class="Li">=</code>’) to specify the most recent mouse
  event (see the <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#MOUSE_SUPPORT">MOUSE
  SUPPORT</a> section) or ‘<code class="Li">{marked}</code>’
  (alternative form ‘<code class="Li">~</code>’) to specify the
  marked pane (see <b class="Ic" title="Ic">select-pane</b>
  <b class="Fl" title="Fl">-m</b>).
<div class="Pp"></div>
Sessions, window and panes are each numbered with a unique ID; session IDs are
  prefixed with a ‘<code class="Li">$</code>’, windows with a
  ‘<code class="Li">@</code>’, and panes with a
  ‘<code class="Li">%</code>’. These are unique and are unchanged
  for the life of the session, window or pane in the
  <b class="Nm" title="Nm">tmux</b> server. The pane ID is passed to the child
  process of the pane in the <code class="Ev" title="Ev">TMUX_PANE</code>
  environment variable. IDs may be displayed using the
  ‘<code class="Li">session_id</code>’,
  ‘<code class="Li">window_id</code>’, or
  ‘<code class="Li">pane_id</code>’ formats (see the
  <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a> section) and the
  <b class="Ic" title="Ic">display-message</b>,
  <b class="Ic" title="Ic">list-sessions</b>,
  <b class="Ic" title="Ic">list-windows</b> or
  <b class="Ic" title="Ic">list-panes</b> commands.
<div class="Pp"></div>
<var class="Ar" title="Ar">shell-command</var> arguments are
  <a class="Xr" title="Xr" href="http://man.openbsd.org/sh.1">sh(1)</a> commands. This may be a single
  argument passed to the shell, for example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">new-window 'vi /etc/passwd'
</pre>
</div>
<div class="Pp"></div>
Will run:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">/bin/sh -c 'vi /etc/passwd'
</pre>
</div>
<div class="Pp"></div>
Additionally, the <b class="Ic" title="Ic">new-window</b>,
  <b class="Ic" title="Ic">new-session</b>,
  <b class="Ic" title="Ic">split-window</b>,
  <b class="Ic" title="Ic">respawn-window</b> and
  <b class="Ic" title="Ic">respawn-pane</b> commands allow
  <var class="Ar" title="Ar">shell-command</var> to be given as multiple
  arguments and executed directly (without ‘<code class="Li">sh
  -c</code>’). This can avoid issues with shell quoting. For example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">$ tmux new-window vi /etc/passwd
</pre>
</div>
<div class="Pp"></div>
Will run <a class="Xr" title="Xr" href="http://man.openbsd.org/vi.1">vi(1)</a> directly without
  invoking the shell.
<div class="Pp"></div>
<var class="Ar" title="Ar">command</var>
  [<span class="Op"><var class="Ar" title="Ar">arguments</var></span>] refers to
  a <b class="Nm" title="Nm">tmux</b> command, passed with the command and
  arguments separately, for example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">bind-key F1 set-window-option force-width 81
</pre>
</div>
<div class="Pp"></div>
Or if using <a class="Xr" title="Xr" href="http://man.openbsd.org/sh.1">sh(1)</a>:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">$ tmux bind-key F1 set-window-option force-width 81
</pre>
</div>
<div class="Pp"></div>
Multiple commands may be specified together as part of a
  <i class="Em" title="Em">command sequence</i>. Each command should be
  separated by spaces and a semicolon; commands are executed sequentially from
  left to right and lines ending with a backslash continue on to the next line,
  except when escaped by another backslash. A literal semicolon may be included
  by escaping it with a backslash (for example, when specifying a command
  sequence to <b class="Ic" title="Ic">bind-key</b>).
<div class="Pp"></div>
Example <b class="Nm" title="Nm">tmux</b> commands include:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">refresh-client -t/dev/ttyp2 
 
rename-session -tfirst newname 
 
set-window-option -t:0 monitor-activity on 
 
new-window ; split-window -d 
 
bind-key R source-file ~/.tmux.conf \; \ 
	display-message "source-file done"
</pre>
</div>
<div class="Pp"></div>
Or from <a class="Xr" title="Xr" href="http://man.openbsd.org/sh.1">sh(1)</a>:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">$ tmux kill-window -t :1 
 
$ tmux new-window \; split-window -d 
 
$ tmux new-session -d 'vi /etc/passwd' \; split-window -d \; attach
</pre>
</div>
<h1 class="Sh" title="Sh" id="CLIENTS_AND_SESSIONS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#CLIENTS_AND_SESSIONS">CLIENTS
  AND SESSIONS</a></h1>
The <b class="Nm" title="Nm">tmux</b> server manages clients, sessions, windows
  and panes. Clients are attached to sessions to interact with them, either when
  they are created with the <b class="Ic" title="Ic">new-session</b> command, or
  later with the <b class="Ic" title="Ic">attach-session</b> command. Each
  session has one or more windows <i class="Em" title="Em">linked</i> into it.
  Windows may be linked to multiple sessions and are made up of one or more
  panes, each of which contains a pseudo terminal. Commands for creating,
  linking and otherwise manipulating windows are covered in the
  <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#WINDOWS_AND_PANES">WINDOWS AND PANES</a>
  section.
<div class="Pp"></div>
The following commands are available to manage clients and sessions:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#attach-session"><b class="Ic" title="Ic" id="attach-session">attach-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-dEr</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">working-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">attach</b>)</div>
    If run from outside <b class="Nm" title="Nm">tmux</b>, create a new client
      in the current terminal and attach it to
      <var class="Ar" title="Ar">target-session</var>. If used from inside,
      switch the current client. If <b class="Fl" title="Fl">-d</b> is
      specified, any other clients attached to the session are detached.
      <b class="Fl" title="Fl">-r</b> signifies the client is read-only (only
      keys bound to the <b class="Ic" title="Ic">detach-client</b> or
      <b class="Ic" title="Ic">switch-client</b> commands have any effect)
    <div class="Pp"></div>
    If no server is started, <b class="Ic" title="Ic">attach-session</b> will
      attempt to start it; this will fail unless sessions are created in the
      configuration file.
    <div class="Pp"></div>
    The <var class="Ar" title="Ar">target-session</var> rules for
      <b class="Ic" title="Ic">attach-session</b> are slightly adjusted: if
      <b class="Nm" title="Nm">tmux</b> needs to select the most recently used
      session, it will prefer the most recently used
      <i class="Em" title="Em">unattached</i> session.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-c</b> will set the session working directory (used
      for new windows) to <var class="Ar" title="Ar">working-directory</var>.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-E</b> is used, the
      <b class="Ic" title="Ic">update-environment</b> option will not be
      applied.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#detach-client"><b class="Ic" title="Ic" id="detach-client">detach-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-aP</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-E</b>
    <var class="Ar" title="Ar">shell-command</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">target-session</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">detach</b>)</div>
    Detach the current client if bound to a key, the client specified with
      <b class="Fl" title="Fl">-t</b>, or all clients currently attached to the
      session specified by <b class="Fl" title="Fl">-s</b>. The
      <b class="Fl" title="Fl">-a</b> option kills all but the client given with
      <b class="Fl" title="Fl">-t</b>. If <b class="Fl" title="Fl">-P</b> is
      given, send SIGHUP to the parent process of the client, typically causing
      it to exit. With <b class="Fl" title="Fl">-E</b>, run
      <var class="Ar" title="Ar">shell-command</var> to replace the client.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#has-session"><b class="Ic" title="Ic" id="has-session">has-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">has</b>)</div>
    Report an error and exit with 1 if the specified session does not exist. If
      it does exist, exit with 0.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#kill-server"><b class="Ic" title="Ic" id="kill-server">kill-server</b></a></dt>
  <dd class="It-tag">Kill the <b class="Nm" title="Nm">tmux</b> server and
      clients and destroy all sessions.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#kill-session"><b class="Ic" title="Ic" id="kill-session">kill-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-aC</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">Destroy the given session, closing any windows linked to it
      and no other sessions, and detaching all clients attached to it. If
      <b class="Fl" title="Fl">-a</b> is given, all sessions but the specified
      one is killed. The <b class="Fl" title="Fl">-C</b> flag clears alerts
      (bell, activity, or silence) in all windows linked to the session.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-clients"><b class="Ic" title="Ic" id="list-clients">list-clients</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lsc</b>)</div>
    List all clients attached to the server. For the meaning of the
      <b class="Fl" title="Fl">-F</b> flag, see the
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a> section. If
      <var class="Ar" title="Ar">target-session</var> is specified, list only
      clients connected to that session.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-commands"><b class="Ic" title="Ic" id="list-commands">list-commands</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lscm</b>)</div>
    List the syntax of all commands supported by
      <b class="Nm" title="Nm">tmux</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-sessions"><b class="Ic" title="Ic" id="list-sessions">list-sessions</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">ls</b>)</div>
    List all sessions managed by the server. For the meaning of the
      <b class="Fl" title="Fl">-F</b> flag, see the
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a> section.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#lock-client"><b class="Ic" title="Ic" id="lock-client">lock-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lockc</b>)</div>
    Lock <var class="Ar" title="Ar">target-client</var>, see the
      <b class="Ic" title="Ic">lock-server</b> command.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#lock-session"><b class="Ic" title="Ic" id="lock-session">lock-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">locks</b>)</div>
    Lock all clients attached to
      <var class="Ar" title="Ar">target-session</var>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#new-session"><b class="Ic" title="Ic" id="new-session">new-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-AdDEP</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">start-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-n</b>
    <var class="Ar" title="Ar">window-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">session-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">group-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-x</b>
    <var class="Ar" title="Ar">width</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-y</b>
    <var class="Ar" title="Ar">height</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">new</b>)</div>
    Create a new session with name
      <var class="Ar" title="Ar">session-name</var>.
    <div class="Pp"></div>
    The new session is attached to the current terminal unless
      <b class="Fl" title="Fl">-d</b> is given.
      <var class="Ar" title="Ar">window-name</var> and
      <var class="Ar" title="Ar">shell-command</var> are the name of and shell
      command to execute in the initial window. With
      <b class="Fl" title="Fl">-d</b>, the initial size is 80 x 24;
      <b class="Fl" title="Fl">-x</b> and <b class="Fl" title="Fl">-y</b> can be
      used to specify a different size.
    <div class="Pp"></div>
    If run from a terminal, any
      <a class="Xr" title="Xr" href="http://man.openbsd.org/termios.4">termios(4)</a> special
      characters are saved and used for new windows in the new session.
    <div class="Pp"></div>
    The <b class="Fl" title="Fl">-A</b> flag makes
      <b class="Ic" title="Ic">new-session</b> behave like
      <b class="Ic" title="Ic">attach-session</b> if
      <var class="Ar" title="Ar">session-name</var> already exists; in this
      case, <b class="Fl" title="Fl">-D</b> behaves like
      <b class="Fl" title="Fl">-d</b> to
      <b class="Ic" title="Ic">attach-session</b>.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-t</b> is given, it specifies a
      <b class="Ic" title="Ic">session group</b>. Sessions in the same group
      share the same set of windows - new windows are linked to all sessions in
      the group and any windows closed removed from all sessions. The current
      and previous window and any session options remain independent and any
      session in a group may be killed without affecting the others. The
      <var class="Ar" title="Ar">group-name</var> argument may be:
    <ol class="Bl-enum">
      <li class="It-enum">the name of an existing group, in which case the new
          session is added to that group;</li>
      <li class="It-enum">the name of an existing session - the new session is
          added to the same group as that session, creating a new group if
          necessary;</li>
      <li class="It-enum">the name for a new group containing only the new
          session.</li>
    </ol>
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-n</b> and
      <var class="Ar" title="Ar">shell-command</var> are invalid if
      <b class="Fl" title="Fl">-t</b> is used.
    <div class="Pp"></div>
    The <b class="Fl" title="Fl">-P</b> option prints information about the new
      session after it has been created. By default, it uses the format
      ‘<code class="Li">#{session_name}:</code>’ but a different
      format may be specified with <b class="Fl" title="Fl">-F</b>.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-E</b> is used, the
      <b class="Ic" title="Ic">update-environment</b> option will not be
      applied.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#refresh-client"><b class="Ic" title="Ic" id="refresh-client">refresh-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-C</b>
    <var class="Ar" title="Ar">width,height</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-S</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">refresh</b>)</div>
    Refresh the current client if bound to a key, or a single client if one is
      given with <b class="Fl" title="Fl">-t</b>. If
      <b class="Fl" title="Fl">-S</b> is specified, only update the client's
      status line.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-C</b> sets the width and height of a control
      client.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#rename-session"><b class="Ic" title="Ic" id="rename-session">rename-session</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]
    <var class="Ar" title="Ar">new-name</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">rename</b>)</div>
    Rename the session to <var class="Ar" title="Ar">new-name</var>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#show-messages"><b class="Ic" title="Ic" id="show-messages">show-messages</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-JT</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">showmsgs</b>)</div>
    Show client messages or server information. Any messages displayed on the
      status line are saved in a per-client message log, up to a maximum of the
      limit set by the <var class="Ar" title="Ar">message-limit</var> server
      option. With <b class="Fl" title="Fl">-t</b>, display the log for
      <var class="Ar" title="Ar">target-client</var>.
      <b class="Fl" title="Fl">-J</b> and <b class="Fl" title="Fl">-T</b> show
      debugging information about jobs and terminals.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#source-file"><b class="Ic" title="Ic" id="source-file">source-file</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-q</b></span>]
    <var class="Ar" title="Ar">path</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">source</b>)</div>
    Execute commands from <var class="Ar" title="Ar">path</var> (which may be a
      <a class="Xr" title="Xr" href="http://man.openbsd.org/glob.3">glob(3)</a> pattern). If
      <b class="Fl" title="Fl">-q</b> is given, no error will be returned if
      <var class="Ar" title="Ar">path</var> does not exist.
    <div class="Pp"></div>
    Within a configuration file, commands may be made conditional by surrounding
      them with <i class="Em" title="Em">%if</i> and
      <i class="Em" title="Em">%endif</i> lines. Additional
      <i class="Em" title="Em">%elif</i> and <i class="Em" title="Em">%else</i>
      lines may also be used. The argument to <i class="Em" title="Em">%if</i>
      and <i class="Em" title="Em">%elif</i> is expanded as a format and if it
      evaluates to false (zero or empty), subsequent lines are ignored until the
      next <i class="Em" title="Em">%elif</i>,
      <i class="Em" title="Em">%else</i> or <i class="Em" title="Em">%endif</i>.
      For example:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">%if #{==:#{host},myhost} 
set -g status-style bg=red 
%elif #{==:#{host},myotherhost} 
set -g status-style bg=green 
%else 
set -g status-style bg=blue 
%endif
    </pre>
    </div>
    <div class="Pp"></div>
    Will change the status line to red if running on
      ‘<code class="Li">myhost</code>’, green if running on
      ‘<code class="Li">myotherhost</code>’, or blue if running on
      another host.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#start-server"><b class="Ic" title="Ic" id="start-server">start-server</b></a></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">start</b>)</div>
    Start the <b class="Nm" title="Nm">tmux</b> server, if not already running,
      without creating any sessions.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#suspend-client"><b class="Ic" title="Ic" id="suspend-client">suspend-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">suspendc</b>)</div>
    Suspend a client by sending <code class="Dv" title="Dv">SIGTSTP</code> (tty
      stop).</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#switch-client"><b class="Ic" title="Ic" id="switch-client">switch-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-Elnpr</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">target-client</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-T</b>
    <var class="Ar" title="Ar">key-table</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">switchc</b>)</div>
    Switch the current session for client
      <var class="Ar" title="Ar">target-client</var> to
      <var class="Ar" title="Ar">target-session</var>. If
      <b class="Fl" title="Fl">-l</b>, <b class="Fl" title="Fl">-n</b> or
      <b class="Fl" title="Fl">-p</b> is used, the client is moved to the last,
      next or previous session respectively. <b class="Fl" title="Fl">-r</b>
      toggles whether a client is read-only (see the
      <b class="Ic" title="Ic">attach-session</b> command).
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-E</b> is used,
      <b class="Ic" title="Ic">update-environment</b> option will not be
      applied.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-T</b> sets the client's key table; the next key
      from the client will be interpreted from
      <var class="Ar" title="Ar">key-table</var>. This may be used to configure
      multiple prefix keys, or to bind commands to sequences of keys. For
      example, to make typing ‘<code class="Li">abc</code>’ run
      the <b class="Ic" title="Ic">list-keys</b> command:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">bind-key -Ttable2 c list-keys 
bind-key -Ttable1 b switch-client -Ttable2 
bind-key -Troot   a switch-client -Ttable1
    </pre>
    </div>
  </dd>
</dl>
<h1 class="Sh" title="Sh" id="WINDOWS_AND_PANES"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#WINDOWS_AND_PANES">WINDOWS
  AND PANES</a></h1>
A <b class="Nm" title="Nm">tmux</b> window may be in one of two modes. The
  default permits direct access to the terminal attached to the window. The
  other is copy mode, which permits a section of a window or its history to be
  copied to a <i class="Em" title="Em">paste buffer</i> for later insertion into
  another window. This mode is entered with the
  <b class="Ic" title="Ic">copy-mode</b> command, bound to
  ‘<code class="Li">[</code>’ by default. It is also entered when
  a command that produces output, such as
  <b class="Ic" title="Ic">list-keys</b>, is executed from a key binding.
<div class="Pp"></div>
Commands are sent to copy mode using the <b class="Fl" title="Fl">-X</b> flag to
  the <b class="Ic" title="Ic">send-keys</b> command. When a key is pressed,
  copy mode automatically uses one of two key tables, depending on the
  <b class="Ic" title="Ic">mode-keys</b> option:
  <b class="Ic" title="Ic">copy-mode</b> for emacs, or
  <b class="Ic" title="Ic">copy-mode-vi</b> for vi. Key tables may be viewed
  with the <b class="Ic" title="Ic">list-keys</b> command.
<div class="Pp"></div>
The following commands are supported in copy mode:
<table class="Bl-column" style="margin-left: 6.00ex;">
  <colgroup>
    <col style="width: 42.60ex;">
    <col style="width: 17.40ex;">
    <col style="min-width: 5.00ex;">
  </colgroup>
  <tbody><tr class="It-column">
    <td class="It-column"><b class="Sy" title="Sy">Command</b></td>
    <td class="It-column"><b class="Sy" title="Sy">vi</b></td>
    <td class="It-column"><b class="Sy" title="Sy">emacs</b></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#append-selection"><code class="Li" id="append-selection">append-selection</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#append-selection-and-cancel"><code class="Li" id="append-selection-and-cancel">append-selection-and-cancel</code></a></td>
    <td class="It-column">A</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#back-to-indentation"><code class="Li" id="back-to-indentation">back-to-indentation</code></a></td>
    <td class="It-column">^</td>
    <td class="It-column">M-m</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#begin-selection"><code class="Li" id="begin-selection">begin-selection</code></a></td>
    <td class="It-column">Space</td>
    <td class="It-column">C-Space</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#bottom-line"><code class="Li" id="bottom-line">bottom-line</code></a></td>
    <td class="It-column">L</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#cancel"><code class="Li" id="cancel">cancel</code></a></td>
    <td class="It-column">q</td>
    <td class="It-column">Escape</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#clear-selection"><code class="Li" id="clear-selection">clear-selection</code></a></td>
    <td class="It-column">Escape</td>
    <td class="It-column">C-g</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-end-of-line"><code class="Li" id="copy-end-of-line">copy-end-of-line</code></a></td>
    <td class="It-column">D</td>
    <td class="It-column">C-k</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-line"><code class="Li" id="copy-line">copy-line</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-pipe_&lt;command&gt;"><code class="Li" id="copy-pipe_&lt;command&gt;">copy-pipe
      &lt;command&gt;</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-pipe-and-cancel_&lt;command&gt;"><code class="Li" id="copy-pipe-and-cancel_&lt;command&gt;">copy-pipe-and-cancel
      &lt;command&gt;</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-selection"><code class="Li" id="copy-selection">copy-selection</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-selection-and-cancel"><code class="Li" id="copy-selection-and-cancel">copy-selection-and-cancel</code></a></td>
    <td class="It-column">Enter</td>
    <td class="It-column">M-w</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#cursor-down"><code class="Li" id="cursor-down">cursor-down</code></a></td>
    <td class="It-column">j</td>
    <td class="It-column">Down</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#cursor-left"><code class="Li" id="cursor-left">cursor-left</code></a></td>
    <td class="It-column">h</td>
    <td class="It-column">Left</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#cursor-right"><code class="Li" id="cursor-right">cursor-right</code></a></td>
    <td class="It-column">l</td>
    <td class="It-column">Right</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#cursor-up"><code class="Li" id="cursor-up">cursor-up</code></a></td>
    <td class="It-column">k</td>
    <td class="It-column">Up</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#end-of-line"><code class="Li" id="end-of-line">end-of-line</code></a></td>
    <td class="It-column">$</td>
    <td class="It-column">C-e</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#goto-line_&lt;line&gt;"><code class="Li" id="goto-line_&lt;line&gt;">goto-line
      &lt;line&gt;</code></a></td>
    <td class="It-column">:</td>
    <td class="It-column">g</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#halfpage-down"><code class="Li" id="halfpage-down">halfpage-down</code></a></td>
    <td class="It-column">C-d</td>
    <td class="It-column">M-Down</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#halfpage-down-and-cancel"><code class="Li" id="halfpage-down-and-cancel">halfpage-down-and-cancel</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#halfpage-up"><code class="Li" id="halfpage-up">halfpage-up</code></a></td>
    <td class="It-column">C-u</td>
    <td class="It-column">M-Up</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#history-bottom"><code class="Li" id="history-bottom">history-bottom</code></a></td>
    <td class="It-column">G</td>
    <td class="It-column">M-&gt;</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#history-top"><code class="Li" id="history-top">history-top</code></a></td>
    <td class="It-column">g</td>
    <td class="It-column">M-&lt;</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-again"><code class="Li" id="jump-again">jump-again</code></a></td>
    <td class="It-column">;</td>
    <td class="It-column">;</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-backward_&lt;to&gt;"><code class="Li" id="jump-backward_&lt;to&gt;">jump-backward
      &lt;to&gt;</code></a></td>
    <td class="It-column">F</td>
    <td class="It-column">F</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-forward_&lt;to&gt;"><code class="Li" id="jump-forward_&lt;to&gt;">jump-forward
      &lt;to&gt;</code></a></td>
    <td class="It-column">f</td>
    <td class="It-column">f</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-reverse"><code class="Li" id="jump-reverse">jump-reverse</code></a></td>
    <td class="It-column">,</td>
    <td class="It-column">,</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-to-backward_&lt;to&gt;"><code class="Li" id="jump-to-backward_&lt;to&gt;">jump-to-backward
      &lt;to&gt;</code></a></td>
    <td class="It-column">T</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#jump-to-forward_&lt;to&gt;"><code class="Li" id="jump-to-forward_&lt;to&gt;">jump-to-forward
      &lt;to&gt;</code></a></td>
    <td class="It-column">t</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#middle-line"><code class="Li" id="middle-line">middle-line</code></a></td>
    <td class="It-column">M</td>
    <td class="It-column">M-r</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-paragraph"><code class="Li" id="next-paragraph">next-paragraph</code></a></td>
    <td class="It-column">}</td>
    <td class="It-column">M-}</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-space"><code class="Li" id="next-space">next-space</code></a></td>
    <td class="It-column">W</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-space-end"><code class="Li" id="next-space-end">next-space-end</code></a></td>
    <td class="It-column">E</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-word"><code class="Li" id="next-word">next-word</code></a></td>
    <td class="It-column">w</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-word-end"><code class="Li" id="next-word-end">next-word-end</code></a></td>
    <td class="It-column">e</td>
    <td class="It-column">M-f</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#other-end"><code class="Li" id="other-end">other-end</code></a></td>
    <td class="It-column">o</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#page-down"><code class="Li" id="page-down">page-down</code></a></td>
    <td class="It-column">C-f</td>
    <td class="It-column">PageDown</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#page-down-and-cancel"><code class="Li" id="page-down-and-cancel">page-down-and-cancel</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#page-up"><code class="Li" id="page-up">page-up</code></a></td>
    <td class="It-column">C-b</td>
    <td class="It-column">PageUp</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#previous-paragraph"><code class="Li" id="previous-paragraph">previous-paragraph</code></a></td>
    <td class="It-column">{</td>
    <td class="It-column">M-{</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#previous-space"><code class="Li" id="previous-space">previous-space</code></a></td>
    <td class="It-column">B</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#previous-word"><code class="Li" id="previous-word">previous-word</code></a></td>
    <td class="It-column">b</td>
    <td class="It-column">M-b</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#rectangle-toggle"><code class="Li" id="rectangle-toggle">rectangle-toggle</code></a></td>
    <td class="It-column">v</td>
    <td class="It-column">R</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#scroll-down"><code class="Li" id="scroll-down">scroll-down</code></a></td>
    <td class="It-column">C-e</td>
    <td class="It-column">C-Down</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#scroll-down-and-cancel"><code class="Li" id="scroll-down-and-cancel">scroll-down-and-cancel</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#scroll-up"><code class="Li" id="scroll-up">scroll-up</code></a></td>
    <td class="It-column">C-y</td>
    <td class="It-column">C-Up</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-again"><code class="Li" id="search-again">search-again</code></a></td>
    <td class="It-column">n</td>
    <td class="It-column">n</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-backward_&lt;for&gt;"><code class="Li" id="search-backward_&lt;for&gt;">search-backward
      &lt;for&gt;</code></a></td>
    <td class="It-column">?</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-forward_&lt;for&gt;"><code class="Li" id="search-forward_&lt;for&gt;">search-forward
      &lt;for&gt;</code></a></td>
    <td class="It-column">/</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-backward-incremental_&lt;for&gt;"><code class="Li" id="search-backward-incremental_&lt;for&gt;">search-backward-incremental
      &lt;for&gt;</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">C-r</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-forward-incremental_&lt;for&gt;"><code class="Li" id="search-forward-incremental_&lt;for&gt;">search-forward-incremental
      &lt;for&gt;</code></a></td>
    <td class="It-column"></td>
    <td class="It-column">C-s</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#search-reverse"><code class="Li" id="search-reverse">search-reverse</code></a></td>
    <td class="It-column">N</td>
    <td class="It-column">N</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#select-line"><code class="Li" id="select-line">select-line</code></a></td>
    <td class="It-column">V</td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#start-of-line"><code class="Li" id="start-of-line">start-of-line</code></a></td>
    <td class="It-column">0</td>
    <td class="It-column">C-a</td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#stop-selection"><code class="Li" id="stop-selection">stop-selection</code></a></td>
    <td class="It-column"></td>
    <td class="It-column"></td>
  </tr>
  <tr class="It-column">
    <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#top-line"><code class="Li" id="top-line">top-line</code></a></td>
    <td class="It-column">H</td>
    <td class="It-column">M-R</td>
  </tr>
</tbody></table>
<div class="Pp"></div>
The ‘<code class="Li">-and-cancel</code>’ variants of some
  commands exit copy mode after they have completed (for copy commands) or when
  the cursor reaches the bottom (for scrolling commands).
<div class="Pp"></div>
The next and previous word keys use space and the
  ‘<code class="Li">-</code>’,
  ‘<code class="Li">_</code>’ and
  ‘<code class="Li">@</code>’ characters as word delimiters by
  default, but this can be adjusted by setting the
  <i class="Em" title="Em">word-separators</i> session option. Next word moves
  to the start of the next word, next word end to the end of the next word and
  previous word to the start of the previous word. The three next and previous
  space keys work similarly but use a space alone as the word separator.
<div class="Pp"></div>
The jump commands enable quick movement within a line. For instance, typing
  ‘<code class="Li">f</code>’ followed by
  ‘<code class="Li">/</code>’ will move the cursor to the next
  ‘<code class="Li">/</code>’ character on the current line. A
  ‘<code class="Li">;</code>’ will then jump to the next
  occurrence.
<div class="Pp"></div>
Commands in copy mode may be prefaced by an optional repeat count. With vi key
  bindings, a prefix is entered using the number keys; with emacs, the Alt
  (meta) key and a number begins prefix entry.
<div class="Pp"></div>
The synopsis for the <b class="Ic" title="Ic">copy-mode</b> command is:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#copy-mode"><b class="Ic" title="Ic" id="copy-mode">copy-mode</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-Meu</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]</dt>
  <dd class="It-tag">Enter copy mode. The <b class="Fl" title="Fl">-u</b> option
      scrolls one page up. <b class="Fl" title="Fl">-M</b> begins a mouse drag
      (only valid if bound to a mouse key binding, see
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#MOUSE_SUPPORT">MOUSE SUPPORT</a>).
      <b class="Fl" title="Fl">-e</b> specifies that scrolling to the bottom of
      the history (to the visible screen) should exit copy mode. While in copy
      mode, pressing a key other than those used for scrolling will disable this
      behaviour. This is intended to allow fast scrolling through a pane's
      history, for example with:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">bind PageUp copy-mode -eu
    </pre>
    </div>
  </dd>
</dl>
<div class="Pp"></div>
Each window displayed by <b class="Nm" title="Nm">tmux</b> may be split into one
  or more <i class="Em" title="Em">panes</i>; each pane takes up a certain area
  of the display and is a separate terminal. A window may be split into panes
  using the <b class="Ic" title="Ic">split-window</b> command. Windows may be
  split horizontally (with the <b class="Fl" title="Fl">-h</b> flag) or
  vertically. Panes may be resized with the
  <b class="Ic" title="Ic">resize-pane</b> command (bound to
  ‘<code class="Li">C-Up</code>’,
  ‘<code class="Li">C-Down</code>’
  ‘<code class="Li">C-Left</code>’ and
  ‘<code class="Li">C-Right</code>’ by default), the current pane
  may be changed with the <b class="Ic" title="Ic">select-pane</b> command and
  the <b class="Ic" title="Ic">rotate-window</b> and
  <b class="Ic" title="Ic">swap-pane</b> commands may be used to swap panes
  without changing their position. Panes are numbered beginning from zero in the
  order they are created.
<div class="Pp"></div>
A number of preset <i class="Em" title="Em">layouts</i> are available. These may
  be selected with the <b class="Ic" title="Ic">select-layout</b> command or
  cycled with <b class="Ic" title="Ic">next-layout</b> (bound to
  ‘<code class="Li">Space</code>’ by default); once a layout is
  chosen, panes within it may be moved and resized as normal.
<div class="Pp"></div>
The following layouts are supported:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#even-horizontal"><b class="Ic" title="Ic" id="even-horizontal">even-horizontal</b></a></dt>
  <dd class="It-tag">Panes are spread out evenly from left to right across the
      window.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#even-vertical"><b class="Ic" title="Ic" id="even-vertical">even-vertical</b></a></dt>
  <dd class="It-tag">Panes are spread evenly from top to bottom.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#main-horizontal"><b class="Ic" title="Ic" id="main-horizontal">main-horizontal</b></a></dt>
  <dd class="It-tag">A large (main) pane is shown at the top of the window and
      the remaining panes are spread from left to right in the leftover space at
      the bottom. Use the <i class="Em" title="Em">main-pane-height</i> window
      option to specify the height of the top pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#main-vertical"><b class="Ic" title="Ic" id="main-vertical">main-vertical</b></a></dt>
  <dd class="It-tag">Similar to <b class="Ic" title="Ic">main-horizontal</b> but
      the large pane is placed on the left and the others spread from top to
      bottom along the right. See the
      <i class="Em" title="Em">main-pane-width</i> window option.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#tiled"><b class="Ic" title="Ic" id="tiled">tiled</b></a></dt>
  <dd class="It-tag">Panes are spread out as evenly as possible over the window
      in both rows and columns.</dd>
</dl>
<div class="Pp"></div>
In addition, <b class="Ic" title="Ic">select-layout</b> may be used to apply a
  previously used layout - the <b class="Ic" title="Ic">list-windows</b> command
  displays the layout of each window in a form suitable for use with
  <b class="Ic" title="Ic">select-layout</b>. For example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">$ tmux list-windows 
0: ksh [159x48] 
    layout: bb62,159x48,0,0{79x48,0,0,79x48,80,0} 
$ tmux select-layout bb62,159x48,0,0{79x48,0,0,79x48,80,0}
</pre>
</div>
<div class="Pp"></div>
<b class="Nm" title="Nm">tmux</b> automatically adjusts the size of the layout
  for the current window size. Note that a layout cannot be applied to a window
  with more panes than that from which the layout was originally defined.
<div class="Pp"></div>
Commands related to windows and panes are as follows:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#break-pane"><b class="Ic" title="Ic" id="break-pane">break-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-dP</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-n</b>
    <var class="Ar" title="Ar">window-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-pane</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">breakp</b>)</div>
    Break <var class="Ar" title="Ar">src-pane</var> off from its containing
      window to make it the only pane in
      <var class="Ar" title="Ar">dst-window</var>. If
      <b class="Fl" title="Fl">-d</b> is given, the new window does not become
      the current window. The <b class="Fl" title="Fl">-P</b> option prints
      information about the new window after it has been created. By default, it
      uses the format
      ‘<code class="Li">#{session_name}:#{window_index}</code>’
      but a different format may be specified with
      <b class="Fl" title="Fl">-F</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#capture-pane"><b class="Ic" title="Ic" id="capture-pane">capture-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-aepPqCJ</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-b</b>
    <var class="Ar" title="Ar">buffer-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-E</b>
    <var class="Ar" title="Ar">end-line</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-S</b>
    <var class="Ar" title="Ar">start-line</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">capturep</b>)</div>
    Capture the contents of a pane. If <b class="Fl" title="Fl">-p</b> is given,
      the output goes to stdout, otherwise to the buffer specified with
      <b class="Fl" title="Fl">-b</b> or a new buffer if omitted. If
      <b class="Fl" title="Fl">-a</b> is given, the alternate screen is used,
      and the history is not accessible. If no alternate screen exists, an error
      will be returned unless <b class="Fl" title="Fl">-q</b> is given. If
      <b class="Fl" title="Fl">-e</b> is given, the output includes escape
      sequences for text and background attributes.
      <b class="Fl" title="Fl">-C</b> also escapes non-printable characters as
      octal \xxx. <b class="Fl" title="Fl">-J</b> joins wrapped lines and
      preserves trailing spaces at each line's end.
      <b class="Fl" title="Fl">-P</b> captures only any output that the pane has
      received that is the beginning of an as-yet incomplete escape sequence.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-S</b> and <b class="Fl" title="Fl">-E</b> specify
      the starting and ending line numbers, zero is the first line of the
      visible pane and negative numbers are lines in the history.
      ‘<code class="Li">-</code>’ to
      <b class="Fl" title="Fl">-S</b> is the start of the history and to
      <b class="Fl" title="Fl">-E</b> the end of the visible pane. The default
      is to capture only the visible contents of the pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#choose-client"><b class="Ic" title="Ic" id="choose-client">choose-client</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-NZ</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-f</b>
    <var class="Ar" title="Ar">filter</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-O</b>
    <var class="Ar" title="Ar">sort-order</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">template</var></span>]</dt>
  <dd class="It-tag">Put a pane into client mode, allowing a client to be
      selected interactively from a list. <b class="Fl" title="Fl">-Z</b> zooms
      the pane. The following keys may be used in client mode:
    <table class="Bl-column" style="margin-left: 6.00ex;">
      <colgroup>
        <col style="width: 6.60ex;">
        <col style="min-width: 8.00ex;">
      </colgroup>
      <tbody><tr class="It-column">
        <td class="It-column"><b class="Sy" title="Sy">Key</b></td>
        <td class="It-column"><b class="Sy" title="Sy">Function</b></td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Enter"><code class="Li" id="Enter">Enter</code></a></td>
        <td class="It-column">Choose selected client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Up"><code class="Li" id="Up">Up</code></a></td>
        <td class="It-column">Select previous client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Down"><code class="Li" id="Down">Down</code></a></td>
        <td class="It-column">Select next client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#C-s"><code class="Li" id="C-s">C-s</code></a></td>
        <td class="It-column">Search by name</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#n"><code class="Li" id="n">n</code></a></td>
        <td class="It-column">Repeat last search</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#t"><code class="Li" id="t">t</code></a></td>
        <td class="It-column">Toggle if client is tagged</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#T"><code class="Li" id="T">T</code></a></td>
        <td class="It-column">Tag no clients</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#C-t"><code class="Li" id="C-t">C-t</code></a></td>
        <td class="It-column">Tag all clients</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#d"><code class="Li" id="d">d</code></a></td>
        <td class="It-column">Detach selected client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#D"><code class="Li" id="D">D</code></a></td>
        <td class="It-column">Detach tagged clients</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#x"><code class="Li" id="x">x</code></a></td>
        <td class="It-column">Detach and HUP selected client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#X"><code class="Li" id="X">X</code></a></td>
        <td class="It-column">Detach and HUP tagged clients</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#z"><code class="Li" id="z">z</code></a></td>
        <td class="It-column">Suspend selected client</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Z"><code class="Li" id="Z">Z</code></a></td>
        <td class="It-column">Suspend tagged clients</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#f"><code class="Li" id="f">f</code></a></td>
        <td class="It-column">Enter a format to filter items</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#O"><code class="Li" id="O">O</code></a></td>
        <td class="It-column">Change sort order</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#v"><code class="Li" id="v">v</code></a></td>
        <td class="It-column">Toggle preview</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#q"><code class="Li" id="q">q</code></a></td>
        <td class="It-column">Exit mode</td>
      </tr>
    </tbody></table>
    <div class="Pp"></div>
    After a client is chosen, ‘<code class="Li">%%</code>’ is
      replaced by the client name in <var class="Ar" title="Ar">template</var>
      and the result executed as a command. If
      <var class="Ar" title="Ar">template</var> is not given,
      "detach-client -t '%%'" is used.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-O</b> specifies the initial sort order: one of
      ‘<code class="Li">name</code>’,
      ‘<code class="Li">size</code>’,
      ‘<code class="Li">creation</code>’, or
      ‘<code class="Li">activity</code>’.
      <b class="Fl" title="Fl">-f</b> specifies an initial filter: the filter is
      a format - if it evaluates to zero, the item in the list is not shown,
      otherwise it is shown. If a filter would lead to an empty list, it is
      ignored. <b class="Fl" title="Fl">-F</b> specifies the format for each
      item in the list. <b class="Fl" title="Fl">-N</b> starts without the
      preview. This command works only if at least one client is attached.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#choose-tree"><b class="Ic" title="Ic" id="choose-tree">choose-tree</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-GNswZ</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-f</b>
    <var class="Ar" title="Ar">filter</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-O</b>
    <var class="Ar" title="Ar">sort-order</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">template</var></span>]</dt>
  <dd class="It-tag">Put a pane into tree mode, where a session, window or pane
      may be chosen interactively from a list. <b class="Fl" title="Fl">-s</b>
      starts with sessions collapsed and <b class="Fl" title="Fl">-w</b> with
      windows collapsed. <b class="Fl" title="Fl">-Z</b> zooms the pane. The
      following keys may be used in tree mode:
    <table class="Bl-column" style="margin-left: 6.00ex;">
      <colgroup>
        <col style="width: 6.60ex;">
        <col style="min-width: 8.00ex;">
      </colgroup>
      <tbody><tr class="It-column">
        <td class="It-column"><b class="Sy" title="Sy">Key</b></td>
        <td class="It-column"><b class="Sy" title="Sy">Function</b></td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Enter"><code class="Li" id="Enter">Enter</code></a></td>
        <td class="It-column">Choose selected item</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Up"><code class="Li" id="Up">Up</code></a></td>
        <td class="It-column">Select previous item</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#Down"><code class="Li" id="Down">Down</code></a></td>
        <td class="It-column">Select next item</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#&lt;"><code class="Li" id="&lt;">&lt;</code></a></td>
        <td class="It-column">Scroll list of previews left</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#&gt;"><code class="Li" id="&gt;">&gt;</code></a></td>
        <td class="It-column">Scroll list of previews right</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#C-s"><code class="Li" id="C-s">C-s</code></a></td>
        <td class="It-column">Search by name</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#n"><code class="Li" id="n">n</code></a></td>
        <td class="It-column">Repeat last search</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#t"><code class="Li" id="t">t</code></a></td>
        <td class="It-column">Toggle if item is tagged</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#T"><code class="Li" id="T">T</code></a></td>
        <td class="It-column">Tag no items</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#C-t"><code class="Li" id="C-t">C-t</code></a></td>
        <td class="It-column">Tag all items</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#:"><code class="Li" id=":">:</code></a></td>
        <td class="It-column">Run a command for each tagged item</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#f"><code class="Li" id="f">f</code></a></td>
        <td class="It-column">Enter a format to filter items</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#O"><code class="Li" id="O">O</code></a></td>
        <td class="It-column">Change sort order</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#v"><code class="Li" id="v">v</code></a></td>
        <td class="It-column">Toggle preview</td>
      </tr>
      <tr class="It-column">
        <td class="It-column"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#q"><code class="Li" id="q">q</code></a></td>
        <td class="It-column">Exit mode</td>
      </tr>
    </tbody></table>
    <div class="Pp"></div>
    After a session, window or pane is chosen,
      ‘<code class="Li">%%</code>’ is replaced by the target in
      <var class="Ar" title="Ar">template</var> and the result executed as a
      command. If <var class="Ar" title="Ar">template</var> is not given,
      "switch-client -t '%%'" is used.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-O</b> specifies the initial sort order: one of
      ‘<code class="Li">index</code>’,
      ‘<code class="Li">name</code>’, or
      ‘<code class="Li">time</code>’.
      <b class="Fl" title="Fl">-f</b> specifies an initial filter: the filter is
      a format - if it evaluates to zero, the item in the list is not shown,
      otherwise it is shown. If a filter would lead to an empty list, it is
      ignored. <b class="Fl" title="Fl">-F</b> specifies the format for each
      item in the tree. <b class="Fl" title="Fl">-N</b> starts without the
      preview. <b class="Fl" title="Fl">-G</b> includes all sessions in any
      session groups in the tree rather than only the first. This command works
      only if at least one client is attached.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#display-panes"><b class="Ic" title="Ic" id="display-panes">display-panes</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-d</b>
    <var class="Ar" title="Ar">duration</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-client</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">template</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">displayp</b>)</div>
    Display a visible indicator of each pane shown by
      <var class="Ar" title="Ar">target-client</var>. See the
      <b class="Ic" title="Ic">display-panes-colour</b> and
      <b class="Ic" title="Ic">display-panes-active-colour</b> session options.
      The indicator is closed when a key is pressed or
      <var class="Ar" title="Ar">duration</var> milliseconds have passed. If
      <b class="Fl" title="Fl">-d</b> is not given,
      <b class="Ic" title="Ic">display-panes-time</b> is used. A duration of
      zero means the indicator stays until a key is pressed. While the indicator
      is on screen, a pane may be chosen with the
      ‘<code class="Li">0</code>’ to
      ‘<code class="Li">9</code>’ keys, which will cause
      <var class="Ar" title="Ar">template</var> to be executed as a command with
      ‘<code class="Li">%%</code>’ substituted by the pane ID. The
      default <var class="Ar" title="Ar">template</var> is "select-pane -t
      '%%'".</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#find-window"><b class="Ic" title="Ic" id="find-window">find-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-CNT</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    <var class="Ar" title="Ar">match-string</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">findw</b>)</div>
    Search for the <a class="Xr" title="Xr" href="http://man.openbsd.org/fnmatch.3">fnmatch(3)</a>
      pattern <var class="Ar" title="Ar">match-string</var> in window names,
      titles, and visible content (but not history). The flags control matching
      behavior: <b class="Fl" title="Fl">-C</b> matches only visible window
      contents, <b class="Fl" title="Fl">-N</b> matches only the window name and
      <b class="Fl" title="Fl">-T</b> matches only the window title. The default
      is <b class="Fl" title="Fl">-CNT</b>.
    <div class="Pp"></div>
    This command works only if at least one client is attached.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#join-pane"><b class="Ic" title="Ic" id="join-pane">join-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-bdhv</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-l</b>
    <var class="Ar" title="Ar">size</var> | <b class="Fl" title="Fl">-p</b>
    <var class="Ar" title="Ar">percentage</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-pane</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">joinp</b>)</div>
    Like <b class="Ic" title="Ic">split-window</b>, but instead of splitting
      <var class="Ar" title="Ar">dst-pane</var> and creating a new pane, split
      it and move <var class="Ar" title="Ar">src-pane</var> into the space. This
      can be used to reverse <b class="Ic" title="Ic">break-pane</b>. The
      <b class="Fl" title="Fl">-b</b> option causes
      <var class="Ar" title="Ar">src-pane</var> to be joined to left of or above
      <var class="Ar" title="Ar">dst-pane</var>.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-s</b> is omitted and a marked pane is present
      (see <b class="Ic" title="Ic">select-pane</b>
      <b class="Fl" title="Fl">-m</b>), the marked pane is used rather than the
      current pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#kill-pane"><b class="Ic" title="Ic" id="kill-pane">kill-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-a</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">killp</b>)</div>
    Destroy the given pane. If no panes remain in the containing window, it is
      also destroyed. The <b class="Fl" title="Fl">-a</b> option kills all but
      the pane given with <b class="Fl" title="Fl">-t</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#kill-window"><b class="Ic" title="Ic" id="kill-window">kill-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-a</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">killw</b>)</div>
    Kill the current window or the window at
      <var class="Ar" title="Ar">target-window</var>, removing it from any
      sessions to which it is linked. The <b class="Fl" title="Fl">-a</b> option
      kills all but the window given with <b class="Fl" title="Fl">-t</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#last-pane"><b class="Ic" title="Ic" id="last-pane">last-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-de</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lastp</b>)</div>
    Select the last (previously selected) pane. <b class="Fl" title="Fl">-e</b>
      enables or <b class="Fl" title="Fl">-d</b> disables input to the
    pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#last-window"><b class="Ic" title="Ic" id="last-window">last-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">last</b>)</div>
    Select the last (previously selected) window. If no
      <var class="Ar" title="Ar">target-session</var> is specified, select the
      last window of the current session.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#link-window"><b class="Ic" title="Ic" id="link-window">link-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-adk</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-window</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">linkw</b>)</div>
    Link the window at <var class="Ar" title="Ar">src-window</var> to the
      specified <var class="Ar" title="Ar">dst-window</var>. If
      <var class="Ar" title="Ar">dst-window</var> is specified and no such
      window exists, the <var class="Ar" title="Ar">src-window</var> is linked
      there. With <b class="Fl" title="Fl">-a</b>, the window is moved to the
      next index up (following windows are moved if necessary). If
      <b class="Fl" title="Fl">-k</b> is given and
      <var class="Ar" title="Ar">dst-window</var> exists, it is killed,
      otherwise an error is generated. If <b class="Fl" title="Fl">-d</b> is
      given, the newly linked window is not selected.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-panes"><b class="Ic" title="Ic" id="list-panes">list-panes</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-as</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lsp</b>)</div>
    If <b class="Fl" title="Fl">-a</b> is given,
      <var class="Ar" title="Ar">target</var> is ignored and all panes on the
      server are listed. If <b class="Fl" title="Fl">-s</b> is given,
      <var class="Ar" title="Ar">target</var> is a session (or the current
      session). If neither is given, <var class="Ar" title="Ar">target</var> is
      a window (or the current window). For the meaning of the
      <b class="Fl" title="Fl">-F</b> flag, see the
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a> section.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-windows"><b class="Ic" title="Ic" id="list-windows">list-windows</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-a</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lsw</b>)</div>
    If <b class="Fl" title="Fl">-a</b> is given, list all windows on the server.
      Otherwise, list windows in the current session or in
      <var class="Ar" title="Ar">target-session</var>. For the meaning of the
      <b class="Fl" title="Fl">-F</b> flag, see the
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a> section.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#move-pane"><b class="Ic" title="Ic" id="move-pane">move-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-bdhv</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-l</b>
    <var class="Ar" title="Ar">size</var> | <b class="Fl" title="Fl">-p</b>
    <var class="Ar" title="Ar">percentage</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-pane</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">movep</b>)</div>
    Like <b class="Ic" title="Ic">join-pane</b>, but
      <var class="Ar" title="Ar">src-pane</var> and
      <var class="Ar" title="Ar">dst-pane</var> may belong to the same
    window.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#move-window"><b class="Ic" title="Ic" id="move-window">move-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-ardk</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-window</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">movew</b>)</div>
    This is similar to <b class="Ic" title="Ic">link-window</b>, except the
      window at <var class="Ar" title="Ar">src-window</var> is moved to
      <var class="Ar" title="Ar">dst-window</var>. With
      <b class="Fl" title="Fl">-r</b>, all windows in the session are renumbered
      in sequential order, respecting the
      <b class="Ic" title="Ic">base-index</b> option.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#new-window"><b class="Ic" title="Ic" id="new-window">new-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-adkP</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">start-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-n</b>
    <var class="Ar" title="Ar">window-name</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">neww</b>)</div>
    Create a new window. With <b class="Fl" title="Fl">-a</b>, the new window is
      inserted at the next index up from the specified
      <var class="Ar" title="Ar">target-window</var>, moving windows up if
      necessary, otherwise <var class="Ar" title="Ar">target-window</var> is the
      new window location.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-d</b> is given, the session does not make the
      new window the current window.
      <var class="Ar" title="Ar">target-window</var> represents the window to be
      created; if the target already exists an error is shown, unless the
      <b class="Fl" title="Fl">-k</b> flag is used, in which case it is
      destroyed. <var class="Ar" title="Ar">shell-command</var> is the command
      to execute. If <var class="Ar" title="Ar">shell-command</var> is not
      specified, the value of the <b class="Ic" title="Ic">default-command</b>
      option is used. <b class="Fl" title="Fl">-c</b> specifies the working
      directory in which the new window is created.
    <div class="Pp"></div>
    When the shell command completes, the window closes. See the
      <b class="Ic" title="Ic">remain-on-exit</b> option to change this
      behaviour.
    <div class="Pp"></div>
    The <code class="Ev" title="Ev">TERM</code> environment variable must be set
      to ‘<code class="Li">screen</code>’ or
      ‘<code class="Li">tmux</code>’ for all programs running
      <i class="Em" title="Em">inside</i> <b class="Nm" title="Nm">tmux</b>. New
      windows will automatically have
      ‘<code class="Li">TERM=screen</code>’ added to their
      environment, but care must be taken not to reset this in shell start-up
      files.
    <div class="Pp"></div>
    The <b class="Fl" title="Fl">-P</b> option prints information about the new
      window after it has been created. By default, it uses the format
      ‘<code class="Li">#{session_name}:#{window_index}</code>’
      but a different format may be specified with
      <b class="Fl" title="Fl">-F</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-layout"><b class="Ic" title="Ic" id="next-layout">next-layout</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">nextl</b>)</div>
    Move a window to the next layout and rearrange the panes to fit.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#next-window"><b class="Ic" title="Ic" id="next-window">next-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-a</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">next</b>)</div>
    Move to the next window in the session. If <b class="Fl" title="Fl">-a</b>
      is used, move to the next window with an alert.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pipe-pane"><b class="Ic" title="Ic" id="pipe-pane">pipe-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-IOo</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">pipep</b>)</div>
    Pipe output sent by the program in
      <var class="Ar" title="Ar">target-pane</var> to a shell command or vice
      versa. A pane may only be connected to one command at a time, any existing
      pipe is closed before <var class="Ar" title="Ar">shell-command</var> is
      executed. The <var class="Ar" title="Ar">shell-command</var> string may
      contain the special character sequences supported by the
      <b class="Ic" title="Ic">status-left</b> option. If no
      <var class="Ar" title="Ar">shell-command</var> is given, the current pipe
      (if any) is closed.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-I</b> and <b class="Fl" title="Fl">-O</b> specify
      which of the <var class="Ar" title="Ar">shell-command</var> output streams
      are connected to the pane: with <b class="Fl" title="Fl">-I</b> stdout is
      connected (so anything <var class="Ar" title="Ar">shell-command</var>
      prints is written to the pane as if it were typed); with
      <b class="Fl" title="Fl">-O</b> stdin is connected (so any output in the
      pane is piped to <var class="Ar" title="Ar">shell-command</var>). Both may
      be used together and if neither are specified,
      <b class="Fl" title="Fl">-O</b> is used.
    <div class="Pp"></div>
    The <b class="Fl" title="Fl">-o</b> option only opens a new pipe if no
      previous pipe exists, allowing a pipe to be toggled with a single key, for
      example:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">bind-key C-p pipe-pane -o 'cat &gt;&gt;~/output.#I-#P'
    </pre>
    </div>
  </dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#previous-layout"><b class="Ic" title="Ic" id="previous-layout">previous-layout</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">prevl</b>)</div>
    Move to the previous layout in the session.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#previous-window"><b class="Ic" title="Ic" id="previous-window">previous-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-a</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">prev</b>)</div>
    Move to the previous window in the session. With
      <b class="Fl" title="Fl">-a</b>, move to the previous window with an
      alert.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#rename-window"><b class="Ic" title="Ic" id="rename-window">rename-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]
    <var class="Ar" title="Ar">new-name</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">renamew</b>)</div>
    Rename the current window, or the window at
      <var class="Ar" title="Ar">target-window</var> if specified, to
      <var class="Ar" title="Ar">new-name</var>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#resize-pane"><b class="Ic" title="Ic" id="resize-pane">resize-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-DLMRUZ</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-x</b>
    <var class="Ar" title="Ar">width</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-y</b>
    <var class="Ar" title="Ar">height</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">adjustment</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">resizep</b>)</div>
    Resize a pane, up, down, left or right by
      <var class="Ar" title="Ar">adjustment</var> with
      <b class="Fl" title="Fl">-U</b>, <b class="Fl" title="Fl">-D</b>,
      <b class="Fl" title="Fl">-L</b> or <b class="Fl" title="Fl">-R</b>, or to
      an absolute size with <b class="Fl" title="Fl">-x</b> or
      <b class="Fl" title="Fl">-y</b>. The
      <var class="Ar" title="Ar">adjustment</var> is given in lines or cells
      (the default is 1).
    <div class="Pp"></div>
    With <b class="Fl" title="Fl">-Z</b>, the active pane is toggled between
      zoomed (occupying the whole of the window) and unzoomed (its normal
      position in the layout).
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-M</b> begins mouse resizing (only valid if bound
      to a mouse key binding, see
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#MOUSE_SUPPORT">MOUSE SUPPORT</a>).</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#respawn-pane"><b class="Ic" title="Ic" id="respawn-pane">respawn-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">start-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-k</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">respawnp</b>)</div>
    Reactivate a pane in which the command has exited (see the
      <b class="Ic" title="Ic">remain-on-exit</b> window option). If
      <var class="Ar" title="Ar">shell-command</var> is not given, the command
      used when the pane was created is executed. The pane must be already
      inactive, unless <b class="Fl" title="Fl">-k</b> is given, in which case
      any existing command is killed. <b class="Fl" title="Fl">-c</b> specifies
      a new working directory for the pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#respawn-window"><b class="Ic" title="Ic" id="respawn-window">respawn-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">start-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-k</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">respawnw</b>)</div>
    Reactivate a window in which the command has exited (see the
      <b class="Ic" title="Ic">remain-on-exit</b> window option). If
      <var class="Ar" title="Ar">shell-command</var> is not given, the command
      used when the window was created is executed. The window must be already
      inactive, unless <b class="Fl" title="Fl">-k</b> is given, in which case
      any existing command is killed. <b class="Fl" title="Fl">-c</b> specifies
      a new working directory for the window.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#rotate-window"><b class="Ic" title="Ic" id="rotate-window">rotate-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-DU</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">rotatew</b>)</div>
    Rotate the positions of the panes within a window, either upward
      (numerically lower) with <b class="Fl" title="Fl">-U</b> or downward
      (numerically higher).</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#select-layout"><b class="Ic" title="Ic" id="select-layout">select-layout</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-Enop</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">layout-name</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">selectl</b>)</div>
    Choose a specific layout for a window. If
      <var class="Ar" title="Ar">layout-name</var> is not given, the last preset
      layout used (if any) is reapplied. <b class="Fl" title="Fl">-n</b> and
      <b class="Fl" title="Fl">-p</b> are equivalent to the
      <b class="Ic" title="Ic">next-layout</b> and
      <b class="Ic" title="Ic">previous-layout</b> commands.
      <b class="Fl" title="Fl">-o</b> applies the last set layout if possible
      (undoes the most recent layout change). <b class="Fl" title="Fl">-E</b>
      spreads the current pane and any panes next to it out evenly.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#select-pane"><b class="Ic" title="Ic" id="select-pane">select-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-DdegLlMmRU</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-P</b>
    <var class="Ar" title="Ar">style</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-T</b>
    <var class="Ar" title="Ar">title</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">selectp</b>)</div>
    Make pane <var class="Ar" title="Ar">target-pane</var> the active pane in
      window <var class="Ar" title="Ar">target-window</var>, or set its style
      (with <b class="Fl" title="Fl">-P</b>). If one of
      <b class="Fl" title="Fl">-D</b>, <b class="Fl" title="Fl">-L</b>,
      <b class="Fl" title="Fl">-R</b>, or <b class="Fl" title="Fl">-U</b> is
      used, respectively the pane below, to the left, to the right, or above the
      target pane is used. <b class="Fl" title="Fl">-l</b> is the same as using
      the <b class="Ic" title="Ic">last-pane</b> command.
      <b class="Fl" title="Fl">-e</b> enables or <b class="Fl" title="Fl">-d</b>
      disables input to the pane.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-m</b> and <b class="Fl" title="Fl">-M</b> are used
      to set and clear the <i class="Em" title="Em">marked pane</i>. There is
      one marked pane at a time, setting a new marked pane clears the last. The
      marked pane is the default target for <b class="Fl" title="Fl">-s</b> to
      <b class="Ic" title="Ic">join-pane</b>,
      <b class="Ic" title="Ic">swap-pane</b> and
      <b class="Ic" title="Ic">swap-window</b>.
    <div class="Pp"></div>
    Each pane has a style: by default the
      <b class="Ic" title="Ic">window-style</b> and
      <b class="Ic" title="Ic">window-active-style</b> options are used,
      <b class="Ic" title="Ic">select-pane</b> <b class="Fl" title="Fl">-P</b>
      sets the style for a single pane. For example, to set the pane 1
      background to red:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">select-pane -t:.1 -P 'bg=red'
    </pre>
    </div>
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-g</b> shows the current pane style.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-T</b> sets the pane title.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#select-window"><b class="Ic" title="Ic" id="select-window">select-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-lnpT</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">selectw</b>)</div>
    Select the window at <var class="Ar" title="Ar">target-window</var>.
      <b class="Fl" title="Fl">-l</b>, <b class="Fl" title="Fl">-n</b> and
      <b class="Fl" title="Fl">-p</b> are equivalent to the
      <b class="Ic" title="Ic">last-window</b>,
      <b class="Ic" title="Ic">next-window</b> and
      <b class="Ic" title="Ic">previous-window</b> commands. If
      <b class="Fl" title="Fl">-T</b> is given and the selected window is
      already the current window, the command behaves like
      <b class="Ic" title="Ic">last-window</b>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#split-window"><b class="Ic" title="Ic" id="split-window">split-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-bdfhvP</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-c</b>
    <var class="Ar" title="Ar">start-directory</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-l</b>
    <var class="Ar" title="Ar">size</var> | <b class="Fl" title="Fl">-p</b>
    <var class="Ar" title="Ar">percentage</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    [<span class="Op"><var class="Ar" title="Ar">shell-command</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-F</b>
    <var class="Ar" title="Ar">format</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">splitw</b>)</div>
    Create a new pane by splitting <var class="Ar" title="Ar">target-pane</var>:
      <b class="Fl" title="Fl">-h</b> does a horizontal split and
      <b class="Fl" title="Fl">-v</b> a vertical split; if neither is specified,
      <b class="Fl" title="Fl">-v</b> is assumed. The
      <b class="Fl" title="Fl">-l</b> and <b class="Fl" title="Fl">-p</b>
      options specify the size of the new pane in lines (for vertical split) or
      in cells (for horizontal split), or as a percentage, respectively. The
      <b class="Fl" title="Fl">-b</b> option causes the new pane to be created
      to the left of or above <var class="Ar" title="Ar">target-pane</var>. The
      <b class="Fl" title="Fl">-f</b> option creates a new pane spanning the
      full window height (with <b class="Fl" title="Fl">-h</b>) or full window
      width (with <b class="Fl" title="Fl">-v</b>), instead of splitting the
      active pane. All other options have the same meaning as for the
      <b class="Ic" title="Ic">new-window</b> command.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#swap-pane"><b class="Ic" title="Ic" id="swap-pane">swap-pane</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-dDU</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-pane</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-pane</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">swapp</b>)</div>
    Swap two panes. If <b class="Fl" title="Fl">-U</b> is used and no source
      pane is specified with <b class="Fl" title="Fl">-s</b>,
      <var class="Ar" title="Ar">dst-pane</var> is swapped with the previous
      pane (before it numerically); <b class="Fl" title="Fl">-D</b> swaps with
      the next pane (after it numerically). <b class="Fl" title="Fl">-d</b>
      instructs <b class="Nm" title="Nm">tmux</b> not to change the active pane.
    <div class="Pp"></div>
    If <b class="Fl" title="Fl">-s</b> is omitted and a marked pane is present
      (see <b class="Ic" title="Ic">select-pane</b>
      <b class="Fl" title="Fl">-m</b>), the marked pane is used rather than the
      current pane.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#swap-window"><b class="Ic" title="Ic" id="swap-window">swap-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-d</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-s</b>
    <var class="Ar" title="Ar">src-window</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">dst-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">swapw</b>)</div>
    This is similar to <b class="Ic" title="Ic">link-window</b>, except the
      source and destination windows are swapped. It is an error if no window
      exists at <var class="Ar" title="Ar">src-window</var>.
    <div class="Pp"></div>
    Like <b class="Ic" title="Ic">swap-pane</b>, if
      <b class="Fl" title="Fl">-s</b> is omitted and a marked pane is present
      (see <b class="Ic" title="Ic">select-pane</b>
      <b class="Fl" title="Fl">-m</b>), the window containing the marked pane is
      used rather than the current window.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#unlink-window"><b class="Ic" title="Ic" id="unlink-window">unlink-window</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-k</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">unlinkw</b>)</div>
    Unlink <var class="Ar" title="Ar">target-window</var>. Unless
      <b class="Fl" title="Fl">-k</b> is given, a window may be unlinked only if
      it is linked to multiple sessions - windows may not be linked to no
      sessions; if <b class="Fl" title="Fl">-k</b> is specified and the window
      is linked to only one session, it is unlinked and destroyed.</dd>
</dl>
<h1 class="Sh" title="Sh" id="KEY_BINDINGS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#KEY_BINDINGS">KEY
  BINDINGS</a></h1>
<b class="Nm" title="Nm">tmux</b> allows a command to be bound to most keys,
  with or without a prefix key. When specifying keys, most represent themselves
  (for example ‘<code class="Li">A</code>’ to
  ‘<code class="Li">Z</code>’). Ctrl keys may be prefixed with
  ‘<code class="Li">C-</code>’ or
  ‘<code class="Li">^</code>’, and Alt (meta) with
  ‘<code class="Li">M-</code>’. In addition, the following special
  key names are accepted: <i class="Em" title="Em">Up</i>,
  <i class="Em" title="Em">Down</i>, <i class="Em" title="Em">Left</i>,
  <i class="Em" title="Em">Right</i>, <i class="Em" title="Em">BSpace</i>,
  <i class="Em" title="Em">BTab</i>, <i class="Em" title="Em">DC</i> (Delete),
  <i class="Em" title="Em">End</i>, <i class="Em" title="Em">Enter</i>,
  <i class="Em" title="Em">Escape</i>, <i class="Em" title="Em">F1</i> to
  <i class="Em" title="Em">F12</i>, <i class="Em" title="Em">Home</i>,
  <i class="Em" title="Em">IC</i> (Insert),
  <i class="Em" title="Em">NPage/PageDown/PgDn</i>,
  <i class="Em" title="Em">PPage/PageUp/PgUp</i>,
  <i class="Em" title="Em">Space</i>, and <i class="Em" title="Em">Tab</i>. Note
  that to bind the ‘<code class="Li">"</code>’ or
  ‘<code class="Li">'</code>’ keys, quotation marks are necessary,
  for example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">bind-key '"' split-window 
bind-key "'" new-window
</pre>
</div>
<div class="Pp"></div>
Commands related to key bindings are as follows:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#bind-key"><b class="Ic" title="Ic" id="bind-key">bind-key</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-nr</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-T</b>
    <var class="Ar" title="Ar">key-table</var></span>]
    <var class="Ar" title="Ar">key</var>
    <var class="Ar" title="Ar">command</var>
    [<span class="Op"><var class="Ar" title="Ar">arguments</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">bind</b>)</div>
    Bind key <var class="Ar" title="Ar">key</var> to
      <var class="Ar" title="Ar">command</var>. Keys are bound in a key table.
      By default (without -T), the key is bound in the
      <i class="Em" title="Em">prefix</i> key table. This table is used for keys
      pressed after the prefix key (for example, by default
      ‘<code class="Li">c</code>’ is bound to
      <b class="Ic" title="Ic">new-window</b> in the
      <i class="Em" title="Em">prefix</i> table, so ‘<code class="Li">C-b
      c</code>’ creates a new window). The
      <i class="Em" title="Em">root</i> table is used for keys pressed without
      the prefix key: binding ‘<code class="Li">c</code>’ to
      <b class="Ic" title="Ic">new-window</b> in the
      <i class="Em" title="Em">root</i> table (not recommended) means a plain
      ‘<code class="Li">c</code>’ will create a new window.
      <b class="Fl" title="Fl">-n</b> is an alias for
      <b class="Fl" title="Fl">-T</b> <var class="Ar" title="Ar">root</var>.
      Keys may also be bound in custom key tables and the
      <b class="Ic" title="Ic">switch-client</b> <b class="Fl" title="Fl">-T</b>
      command used to switch to them from a key binding. The
      <b class="Fl" title="Fl">-r</b> flag indicates this key may repeat, see
      the <b class="Ic" title="Ic">repeat-time</b> option.
    <div class="Pp"></div>
    To view the default bindings and possible commands, see the
      <b class="Ic" title="Ic">list-keys</b> command.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#list-keys"><b class="Ic" title="Ic" id="list-keys">list-keys</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-T</b>
    <var class="Ar" title="Ar">key-table</var></span>]</dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">lsk</b>)</div>
    List all key bindings. Without <b class="Fl" title="Fl">-T</b> all key
      tables are printed. With <b class="Fl" title="Fl">-T</b> only
      <var class="Ar" title="Ar">key-table</var>.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#send-keys"><b class="Ic" title="Ic" id="send-keys">send-keys</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-lMRX</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-N</b>
    <var class="Ar" title="Ar">repeat-count</var></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]
    <var class="Ar" title="Ar">key</var>
    <var class="Ar" title="Ar">...</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">send</b>)</div>
    Send a key or keys to a window. Each argument
      <var class="Ar" title="Ar">key</var> is the name of the key (such as
      ‘<code class="Li">C-a</code>’ or
      ‘<code class="Li">NPage</code>’) to send; if the string is
      not recognised as a key, it is sent as a series of characters. The
      <b class="Fl" title="Fl">-l</b> flag disables key name lookup and sends
      the keys literally. All arguments are sent sequentially from first to
      last. The <b class="Fl" title="Fl">-R</b> flag causes the terminal state
      to be reset.
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-M</b> passes through a mouse event (only valid if
      bound to a mouse key binding, see
      <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#MOUSE_SUPPORT">MOUSE SUPPORT</a>).
    <div class="Pp"></div>
    <b class="Fl" title="Fl">-X</b> is used to send a command into copy mode -
      see the <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#WINDOWS_AND_PANES">WINDOWS AND
      PANES</a> section. <b class="Fl" title="Fl">-N</b> specifies a repeat
      count.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#send-prefix"><b class="Ic" title="Ic" id="send-prefix">send-prefix</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-2</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-pane</var></span>]</dt>
  <dd class="It-tag">Send the prefix key, or with
      <b class="Fl" title="Fl">-2</b> the secondary prefix key, to a window as
      if it was pressed.</dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#unbind-key"><b class="Ic" title="Ic" id="unbind-key">unbind-key</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-an</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-T</b>
    <var class="Ar" title="Ar">key-table</var></span>]
    <var class="Ar" title="Ar">key</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">unbind</b>)</div>
    Unbind the command bound to <var class="Ar" title="Ar">key</var>.
      <b class="Fl" title="Fl">-n</b> and <b class="Fl" title="Fl">-T</b> are
      the same as for <b class="Ic" title="Ic">bind-key</b>. If
      <b class="Fl" title="Fl">-a</b> is present, all key bindings are
    removed.</dd>
</dl>
<h1 class="Sh" title="Sh" id="OPTIONS"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#OPTIONS">OPTIONS</a></h1>
The appearance and behaviour of <b class="Nm" title="Nm">tmux</b> may be
  modified by changing the value of various options. There are three types of
  option: <i class="Em" title="Em">server options</i>,
  <i class="Em" title="Em">session options</i> and
  <i class="Em" title="Em">window options</i>.
<div class="Pp"></div>
The <b class="Nm" title="Nm">tmux</b> server has a set of global options which
  do not apply to any particular window or session. These are altered with the
  <b class="Ic" title="Ic">set-option</b> <b class="Fl" title="Fl">-s</b>
  command, or displayed with the <b class="Ic" title="Ic">show-options</b>
  <b class="Fl" title="Fl">-s</b> command.
<div class="Pp"></div>
In addition, each individual session may have a set of session options, and
  there is a separate set of global session options. Sessions which do not have
  a particular option configured inherit the value from the global session
  options. Session options are set or unset with the
  <b class="Ic" title="Ic">set-option</b> command and may be listed with the
  <b class="Ic" title="Ic">show-options</b> command. The available server and
  session options are listed under the <b class="Ic" title="Ic">set-option</b>
  command.
<div class="Pp"></div>
Similarly, a set of window options is attached to each window, and there is a
  set of global window options from which any unset options are inherited.
  Window options are altered with the
  <b class="Ic" title="Ic">set-window-option</b> command and can be listed with
  the <b class="Ic" title="Ic">show-window-options</b> command. All window
  options are documented with the <b class="Ic" title="Ic">set-window-option</b>
  command.
<div class="Pp"></div>
<b class="Nm" title="Nm">tmux</b> also supports user options which are prefixed
  with a ‘<code class="Li">@</code>’. User options may have any
  name, so long as they are prefixed with
  ‘<code class="Li">@</code>’, and be set to any string. For
  example:
<div class="Pp"></div>
<div class="Bd" style="margin-left: 5.00ex;">
<pre class="Li">$ tmux setw -q @foo "abc123" 
$ tmux showw -v @foo 
abc123
</pre>
</div>
<div class="Pp"></div>
Commands which set options are as follows:
<dl class="Bl-tag">
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#set-option"><b class="Ic" title="Ic" id="set-option">set-option</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-aFgoqsuw</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-session</var> |
    <var class="Ar" title="Ar">target-window</var></span>]
    <var class="Ar" title="Ar">option</var>
    <var class="Ar" title="Ar">value</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">set</b>)</div>
    Set a window option with <b class="Fl" title="Fl">-w</b> (equivalent to the
      <b class="Ic" title="Ic">set-window-option</b> command), a server option
      with <b class="Fl" title="Fl">-s</b>, otherwise a session option. If
      <b class="Fl" title="Fl">-g</b> is given, the global session or window
      option is set. <b class="Fl" title="Fl">-F</b> expands formats in the
      option value. The <b class="Fl" title="Fl">-u</b> flag unsets an option,
      so a session inherits the option from the global options (or with
      <b class="Fl" title="Fl">-g</b>, restores a global option to the default).
    <div class="Pp"></div>
    The <b class="Fl" title="Fl">-o</b> flag prevents setting an option that is
      already set and the <b class="Fl" title="Fl">-q</b> flag suppresses errors
      about unknown or ambiguous options.
    <div class="Pp"></div>
    With <b class="Fl" title="Fl">-a</b>, and if the option expects a string or
      a style, <var class="Ar" title="Ar">value</var> is appended to the
      existing setting. For example:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">set -g status-left "foo" 
set -ag status-left "bar"
    </pre>
    </div>
    <div class="Pp"></div>
    Will result in ‘<code class="Li">foobar</code>’. And:
    <div class="Pp"></div>
    <div class="Bd" style="margin-left: 5.00ex;">
    <pre class="Li">set -g status-style "bg=red" 
set -ag status-style "fg=blue"
    </pre>
    </div>
    <div class="Pp"></div>
    Will result in a red background <i class="Em" title="Em">and</i> blue
      foreground. Without <b class="Fl" title="Fl">-a</b>, the result would be
      the default background and a blue foreground.
    <div class="Pp"></div>
    Available window options are listed under
      <b class="Ic" title="Ic">set-window-option</b>.
    <div class="Pp"></div>
    <var class="Ar" title="Ar">value</var> depends on the option and may be a
      number, a string, or a flag (on, off, or omitted to toggle).
    <div class="Pp"></div>
    Available server options are:
    <dl class="Bl-tag">
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#buffer-limit"><b class="Ic" title="Ic" id="buffer-limit">buffer-limit</b></a>
        <var class="Ar" title="Ar">number</var></dt>
      <dd class="It-tag">Set the number of buffers; as new buffers are added to
          the top of the stack, old ones are removed from the bottom if
          necessary to maintain this maximum length.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#command-alias[]"><b class="Ic" title="Ic" id="command-alias[]">command-alias[]</b></a>
        <var class="Ar" title="Ar">name=value</var></dt>
      <dd class="It-tag">This is an array of custom aliases for commands. If an
          unknown command matches <var class="Ar" title="Ar">name</var>, it is
          replaced with <var class="Ar" title="Ar">value</var>. For example,
          after:
        <div class="Pp"></div>
        <div class="D1"><code class="Li">set -s command-alias[100]
          zoom='resize-pane -Z'</code></div>
        <div class="Pp"></div>
        Using:
        <div class="Pp"></div>
        <div class="D1"><code class="Li">zoom -t:.1</code></div>
        <div class="Pp"></div>
        Is equivalent to:
        <div class="Pp"></div>
        <div class="D1"><code class="Li">resize-pane -Z -t:.1</code></div>
        <div class="Pp"></div>
        Note that aliases are expanded when a command is parsed rather than when
          it is executed, so binding an alias with
          <b class="Ic" title="Ic">bind-key</b> will bind the expanded
        form.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#default-terminal"><b class="Ic" title="Ic" id="default-terminal">default-terminal</b></a>
        <var class="Ar" title="Ar">terminal</var></dt>
      <dd class="It-tag">Set the default terminal for new windows created in
          this session - the default value of the
          <code class="Ev" title="Ev">TERM</code> environment variable. For
          <b class="Nm" title="Nm">tmux</b> to work correctly, this
          <i class="Em" title="Em">must</i> be set to
          ‘<code class="Li">screen</code>’,
          ‘<code class="Li">tmux</code>’ or a derivative of
        them.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#escape-time"><b class="Ic" title="Ic" id="escape-time">escape-time</b></a>
        <var class="Ar" title="Ar">time</var></dt>
      <dd class="It-tag">Set the time in milliseconds for which
          <b class="Nm" title="Nm">tmux</b> waits after an escape is input to
          determine if it is part of a function or meta key sequences. The
          default is 500 milliseconds.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#exit-empty"><b class="Ic" title="Ic" id="exit-empty">exit-empty</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If enabled (the default), the server will exit when
          there are no active sessions.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#exit-unattached"><b class="Ic" title="Ic" id="exit-unattached">exit-unattached</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If enabled, the server will exit when there are no
          attached clients.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#focus-events"><b class="Ic" title="Ic" id="focus-events">focus-events</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">When enabled, focus events are requested from the
          terminal if supported and passed through to applications running in
          <b class="Nm" title="Nm">tmux</b>. Attached clients should be detached
          and attached again after changing this option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#history-file"><b class="Ic" title="Ic" id="history-file">history-file</b></a>
        <var class="Ar" title="Ar">path</var></dt>
      <dd class="It-tag">If not empty, a file to which
          <b class="Nm" title="Nm">tmux</b> will write command prompt history on
          exit and load it from on start.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#message-limit"><b class="Ic" title="Ic" id="message-limit">message-limit</b></a>
        <var class="Ar" title="Ar">number</var></dt>
      <dd class="It-tag">Set the number of error or information messages to save
          in the message log for each client. The default is 100.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#set-clipboard"><b class="Ic" title="Ic" id="set-clipboard">set-clipboard</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">external</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Attempt to set the terminal clipboard content using the
          <a class="Xr" title="Xr" href="http://man.openbsd.org/xterm.1">xterm(1)</a> escape sequence,
          if there is an <i class="Em" title="Em">Ms</i> entry in the
          <a class="Xr" title="Xr" href="http://man.openbsd.org/terminfo.5">terminfo(5)</a>
          description (see the
          <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#TERMINFO_EXTENSIONS">TERMINFO
          EXTENSIONS</a> section).
        <div class="Pp"></div>
        If set to <b class="Ic" title="Ic">on</b>,
          <b class="Nm" title="Nm">tmux</b> will both accept the escape sequence
          to create a buffer and attempt to set the terminal clipboard. If set
          to <b class="Ic" title="Ic">external</b>,
          <b class="Nm" title="Nm">tmux</b> will attempt to set the terminal
          clipboard but ignore attempts by applications to set
          <b class="Nm" title="Nm">tmux</b> buffers. If
          <b class="Ic" title="Ic">off</b>, <b class="Nm" title="Nm">tmux</b>
          will neither accept the clipboard escape sequence nor attempt to set
          the clipboard.
        <div class="Pp"></div>
        Note that this feature needs to be enabled in
          <a class="Xr" title="Xr" href="http://man.openbsd.org/xterm.1">xterm(1)</a> by setting the
          resource:
        <div class="Pp"></div>
        <div class="Bd" style="margin-left: 5.00ex;">
        <pre class="Li">disallowedWindowOps: 20,21,SetXprop
        </pre>
        </div>
        <div class="Pp"></div>
        Or changing this property from the
          <a class="Xr" title="Xr" href="http://man.openbsd.org/xterm.1">xterm(1)</a> interactive menu
          when required.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#terminal-overrides[]"><b class="Ic" title="Ic" id="terminal-overrides[]">terminal-overrides[]</b></a>
        <var class="Ar" title="Ar">string</var></dt>
      <dd class="It-tag">Allow terminal descriptions read using
          <a class="Xr" title="Xr" href="http://man.openbsd.org/terminfo.5">terminfo(5)</a> to be
          overridden. Each entry is a colon-separated string made up of a
          terminal type pattern (matched using
          <a class="Xr" title="Xr" href="http://man.openbsd.org/fnmatch.3">fnmatch(3)</a>) and a set
          of <i class="Em" title="Em">name=value</i> entries.
        <div class="Pp"></div>
        For example, to set the ‘<code class="Li">clear</code>’
          <a class="Xr" title="Xr" href="http://man.openbsd.org/terminfo.5">terminfo(5)</a> entry to
          ‘<code class="Li">\e[H\e[2J</code>’ for all terminal
          types matching ‘<code class="Li">rxvt*</code>’:
        <div class="Pp"></div>
        <div class="D1"><code class="Li">rxvt*:clear=\e[H\e[2J</code></div>
        <div class="Pp"></div>
        The terminal entry value is passed through
          <a class="Xr" title="Xr" href="http://man.openbsd.org/strunvis.3">strunvis(3)</a> before
          interpretation.</dd>
    </dl>
    <div class="Pp"></div>
    Available session options are:
    <dl class="Bl-tag">
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#activity-action"><b class="Ic" title="Ic" id="activity-action">activity-action</b></a>
        [<span class="Op"><b class="Ic" title="Ic">any</b> |
        <b class="Ic" title="Ic">none</b> | <b class="Ic" title="Ic">current</b>
        | <b class="Ic" title="Ic">other</b></span>]</dt>
      <dd class="It-tag">Set action on window activity when
          <b class="Ic" title="Ic">monitor-activity</b> is on.
          <b class="Ic" title="Ic">any</b> means activity in any window linked
          to a session causes a bell or message (depending on
          <b class="Ic" title="Ic">visual-activity</b>) in the current window of
          that session, <b class="Ic" title="Ic">none</b> means all activity is
          ignored (equivalent to <b class="Ic" title="Ic">monitor-activity</b>
          being off), <b class="Ic" title="Ic">current</b> means only activity
          in windows other than the current window are ignored and
          <b class="Ic" title="Ic">other</b> means activity in the current
          window is ignored but not those in other windows.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#assume-paste-time"><b class="Ic" title="Ic" id="assume-paste-time">assume-paste-time</b></a>
        <var class="Ar" title="Ar">milliseconds</var></dt>
      <dd class="It-tag">If keys are entered faster than one in
          <var class="Ar" title="Ar">milliseconds</var>, they are assumed to
          have been pasted rather than typed and
          <b class="Nm" title="Nm">tmux</b> key bindings are not processed. The
          default is one millisecond and zero disables.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#base-index"><b class="Ic" title="Ic" id="base-index">base-index</b></a>
        <var class="Ar" title="Ar">index</var></dt>
      <dd class="It-tag">Set the base index from which an unused index should be
          searched when a new window is created. The default is zero.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#bell-action"><b class="Ic" title="Ic" id="bell-action">bell-action</b></a>
        [<span class="Op"><b class="Ic" title="Ic">any</b> |
        <b class="Ic" title="Ic">none</b> | <b class="Ic" title="Ic">current</b>
        | <b class="Ic" title="Ic">other</b></span>]</dt>
      <dd class="It-tag">Set action on a bell in a window when
          <b class="Ic" title="Ic">monitor-bell</b> is on. The values are the
          same as those for <b class="Ic" title="Ic">activity-action</b>.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#default-command"><b class="Ic" title="Ic" id="default-command">default-command</b></a>
        <var class="Ar" title="Ar">shell-command</var></dt>
      <dd class="It-tag">Set the command used for new windows (if not specified
          when the window is created) to
          <var class="Ar" title="Ar">shell-command</var>, which may be any
          <a class="Xr" title="Xr" href="http://man.openbsd.org/sh.1">sh(1)</a> command. The default
          is an empty string, which instructs <b class="Nm" title="Nm">tmux</b>
          to create a login shell using the value of the
          <b class="Ic" title="Ic">default-shell</b> option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#default-shell"><b class="Ic" title="Ic" id="default-shell">default-shell</b></a>
        <var class="Ar" title="Ar">path</var></dt>
      <dd class="It-tag">Specify the default shell. This is used as the login
          shell for new windows when the
          <b class="Ic" title="Ic">default-command</b> option is set to empty,
          and must be the full path of the executable. When started
          <b class="Nm" title="Nm">tmux</b> tries to set a default value from
          the first suitable of the <code class="Ev" title="Ev">SHELL</code>
          environment variable, the shell returned by
          <a class="Xr" title="Xr" href="http://man.openbsd.org/getpwuid.3">getpwuid(3)</a>, or
          <i class="Pa" title="Pa">/bin/sh</i>. This option should be configured
          when <b class="Nm" title="Nm">tmux</b> is used as a login shell.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#destroy-unattached"><b class="Ic" title="Ic" id="destroy-unattached">destroy-unattached</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If enabled and the session is no longer attached to any
          clients, it is destroyed.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#detach-on-destroy"><b class="Ic" title="Ic" id="detach-on-destroy">detach-on-destroy</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If on (the default), the client is detached when the
          session it is attached to is destroyed. If off, the client is switched
          to the most recently active of the remaining sessions.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#display-panes-active-colour"><b class="Ic" title="Ic" id="display-panes-active-colour">display-panes-active-colour</b></a>
        <var class="Ar" title="Ar">colour</var></dt>
      <dd class="It-tag">Set the colour used by the
          <b class="Ic" title="Ic">display-panes</b> command to show the
          indicator for the active pane.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#display-panes-colour"><b class="Ic" title="Ic" id="display-panes-colour">display-panes-colour</b></a>
        <var class="Ar" title="Ar">colour</var></dt>
      <dd class="It-tag">Set the colour used by the
          <b class="Ic" title="Ic">display-panes</b> command to show the
          indicators for inactive panes.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#display-panes-time"><b class="Ic" title="Ic" id="display-panes-time">display-panes-time</b></a>
        <var class="Ar" title="Ar">time</var></dt>
      <dd class="It-tag">Set the time in milliseconds for which the indicators
          shown by the <b class="Ic" title="Ic">display-panes</b> command
          appear.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#display-time"><b class="Ic" title="Ic" id="display-time">display-time</b></a>
        <var class="Ar" title="Ar">time</var></dt>
      <dd class="It-tag">Set the amount of time for which status line messages
          and other on-screen indicators are displayed. If set to 0, messages
          and indicators are displayed until a key is pressed.
          <var class="Ar" title="Ar">time</var> is in milliseconds.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#history-limit"><b class="Ic" title="Ic" id="history-limit">history-limit</b></a>
        <var class="Ar" title="Ar">lines</var></dt>
      <dd class="It-tag">Set the maximum number of lines held in window history.
          This setting applies only to new windows - existing window histories
          are not resized and retain the limit at the point they were
        created.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#key-table"><b class="Ic" title="Ic" id="key-table">key-table</b></a>
        <var class="Ar" title="Ar">key-table</var></dt>
      <dd class="It-tag">Set the default key table to
          <var class="Ar" title="Ar">key-table</var> instead of
          <i class="Em" title="Em">root</i>.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#lock-after-time"><b class="Ic" title="Ic" id="lock-after-time">lock-after-time</b></a>
        <var class="Ar" title="Ar">number</var></dt>
      <dd class="It-tag">Lock the session (like the
          <b class="Ic" title="Ic">lock-session</b> command) after
          <var class="Ar" title="Ar">number</var> seconds of inactivity. The
          default is not to lock (set to 0).</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#lock-command"><b class="Ic" title="Ic" id="lock-command">lock-command</b></a>
        <var class="Ar" title="Ar">shell-command</var></dt>
      <dd class="It-tag">Command to run when locking each client. The default is
          to run <a class="Xr" title="Xr" href="http://man.openbsd.org/lock.1">lock(1)</a> with
          <b class="Fl" title="Fl">-np</b>.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#message-command-style"><b class="Ic" title="Ic" id="message-command-style">message-command-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set status line message command style, where
          <var class="Ar" title="Ar">style</var> is a comma-separated list of
          characteristics to be specified.
        <div class="Pp"></div>
        These may be ‘<code class="Li">bg=colour</code>’ to set
          the background colour,
          ‘<code class="Li">fg=colour</code>’ to set the
          foreground colour, and a list of attributes as specified below.
        <div class="Pp"></div>
        The colour is one of: <b class="Ic" title="Ic">black</b>,
          <b class="Ic" title="Ic">red</b>, <b class="Ic" title="Ic">green</b>,
          <b class="Ic" title="Ic">yellow</b>,
          <b class="Ic" title="Ic">blue</b>,
          <b class="Ic" title="Ic">magenta</b>,
          <b class="Ic" title="Ic">cyan</b>, <b class="Ic" title="Ic">white</b>,
          aixterm bright variants (if supported:
          <b class="Ic" title="Ic">brightred</b>,
          <b class="Ic" title="Ic">brightgreen</b>, and so on),
          <b class="Ic" title="Ic">colour0</b> to
          <b class="Ic" title="Ic">colour255</b> from the 256-colour set,
          <b class="Ic" title="Ic">default</b>, or a hexadecimal RGB string such
          as ‘<code class="Li">#ffffff</code>’, which chooses the
          closest match from the default 256-colour set.
        <div class="Pp"></div>
        The attributes is either <b class="Ic" title="Ic">none</b> or a
          comma-delimited list of one or more of:
          <b class="Ic" title="Ic">bright</b> (or
          <b class="Ic" title="Ic">bold</b>), <b class="Ic" title="Ic">dim</b>,
          <b class="Ic" title="Ic">underscore</b>,
          <b class="Ic" title="Ic">blink</b>,
          <b class="Ic" title="Ic">reverse</b>,
          <b class="Ic" title="Ic">hidden</b>,
          <b class="Ic" title="Ic">italics</b>, or
          <b class="Ic" title="Ic">strikethrough</b> to turn an attribute on, or
          an attribute prefixed with ‘<code class="Li">no</code>’
          to turn one off.
        <div class="Pp"></div>
        Examples are:
        <div class="Pp"></div>
        <div class="Bd" style="margin-left: 5.00ex;">
        <pre class="Li">fg=yellow,bold,underscore,blink 
bg=black,fg=default,noreverse
        </pre>
        </div>
        <div class="Pp"></div>
        With the <b class="Fl" title="Fl">-a</b> flag to the
          <b class="Ic" title="Ic">set-option</b> command the new style is added
          otherwise the existing style is replaced.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#message-style"><b class="Ic" title="Ic" id="message-style">message-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set status line message style. For how to specify
          <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#mouse"><b class="Ic" title="Ic" id="mouse">mouse</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If on, <b class="Nm" title="Nm">tmux</b> captures the
          mouse and allows mouse events to be bound as key bindings. See the
          <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#MOUSE_SUPPORT">MOUSE SUPPORT</a>
          section for details.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#prefix"><b class="Ic" title="Ic" id="prefix">prefix</b></a>
        <var class="Ar" title="Ar">key</var></dt>
      <dd class="It-tag">Set the key accepted as a prefix key. In addition to
          the standard keys described under
          <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#KEY_BINDINGS">KEY BINDINGS</a>,
          <b class="Ic" title="Ic">prefix</b> can be set to the special key
          ‘<code class="Li">None</code>’ to set no prefix.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#prefix2"><b class="Ic" title="Ic" id="prefix2">prefix2</b></a>
        <var class="Ar" title="Ar">key</var></dt>
      <dd class="It-tag">Set a secondary key accepted as a prefix key. Like
          <b class="Ic" title="Ic">prefix</b>,
          <b class="Ic" title="Ic">prefix2</b> can be set to
          ‘<code class="Li">None</code>’.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#renumber-windows"><b class="Ic" title="Ic" id="renumber-windows">renumber-windows</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">If on, when a window is closed in a session,
          automatically renumber the other windows in numerical order. This
          respects the <b class="Ic" title="Ic">base-index</b> option if it has
          been set. If off, do not renumber the windows.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#repeat-time"><b class="Ic" title="Ic" id="repeat-time">repeat-time</b></a>
        <var class="Ar" title="Ar">time</var></dt>
      <dd class="It-tag">Allow multiple commands to be entered without pressing
          the prefix-key again in the specified
          <var class="Ar" title="Ar">time</var> milliseconds (the default is
          500). Whether a key repeats may be set when it is bound using the
          <b class="Fl" title="Fl">-r</b> flag to
          <b class="Ic" title="Ic">bind-key</b>. Repeat is enabled for the
          default keys bound to the <b class="Ic" title="Ic">resize-pane</b>
          command.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#set-titles"><b class="Ic" title="Ic" id="set-titles">set-titles</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Attempt to set the client terminal title using the
          <i class="Em" title="Em">tsl</i> and <i class="Em" title="Em">fsl</i>
          <a class="Xr" title="Xr" href="http://man.openbsd.org/terminfo.5">terminfo(5)</a> entries if
          they exist. <b class="Nm" title="Nm">tmux</b> automatically sets these
          to the \e]0;...\007 sequence if the terminal appears to be
          <a class="Xr" title="Xr" href="http://man.openbsd.org/xterm.1">xterm(1)</a>. This option is
          off by default.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#set-titles-string"><b class="Ic" title="Ic" id="set-titles-string">set-titles-string</b></a>
        <var class="Ar" title="Ar">string</var></dt>
      <dd class="It-tag">String used to set the window title if
          <b class="Ic" title="Ic">set-titles</b> is on. Formats are expanded,
          see the <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a>
        section.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#silence-action"><b class="Ic" title="Ic" id="silence-action">silence-action</b></a>
        [<span class="Op"><b class="Ic" title="Ic">any</b> |
        <b class="Ic" title="Ic">none</b> | <b class="Ic" title="Ic">current</b>
        | <b class="Ic" title="Ic">other</b></span>]</dt>
      <dd class="It-tag">Set action on window silence when
          <b class="Ic" title="Ic">monitor-silence</b> is on. The values are the
          same as those for <b class="Ic" title="Ic">activity-action</b>.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status"><b class="Ic" title="Ic" id="status">status</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Show or hide the status line.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-interval"><b class="Ic" title="Ic" id="status-interval">status-interval</b></a>
        <var class="Ar" title="Ar">interval</var></dt>
      <dd class="It-tag">Update the status line every
          <var class="Ar" title="Ar">interval</var> seconds. By default, updates
          will occur every 15 seconds. A setting of zero disables redrawing at
          interval.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-justify"><b class="Ic" title="Ic" id="status-justify">status-justify</b></a>
        [<span class="Op"><b class="Ic" title="Ic">left</b> |
        <b class="Ic" title="Ic">centre</b> |
        <b class="Ic" title="Ic">right</b></span>]</dt>
      <dd class="It-tag">Set the position of the window list component of the
          status line: left, centre or right justified.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-keys"><b class="Ic" title="Ic" id="status-keys">status-keys</b></a>
        [<span class="Op"><b class="Ic" title="Ic">vi</b> |
        <b class="Ic" title="Ic">emacs</b></span>]</dt>
      <dd class="It-tag">Use vi or emacs-style key bindings in the status line,
          for example at the command prompt. The default is emacs, unless the
          <code class="Ev" title="Ev">VISUAL</code> or
          <code class="Ev" title="Ev">EDITOR</code> environment variables are
          set and contain the string
        ‘<code class="Li">vi</code>’.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-left"><b class="Ic" title="Ic" id="status-left">status-left</b></a>
        <var class="Ar" title="Ar">string</var></dt>
      <dd class="It-tag">Display <var class="Ar" title="Ar">string</var> (by
          default the session name) to the left of the status line.
          <var class="Ar" title="Ar">string</var> will be passed through
          <a class="Xr" title="Xr" href="http://man.openbsd.org/strftime.3">strftime(3)</a> and
          formats (see <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a>)
          will be expanded. It may also contain the special character sequence
          #[] to change the colour or attributes, for example
          ‘<code class="Li">#[fg=red,bright]</code>’ to set a
          bright red foreground. See the
          <b class="Ic" title="Ic">message-command-style</b> option for a
          description of colours and attributes.
        <div class="Pp"></div>
        For details on how the names and titles can be set see the
          <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#NAMES_AND_TITLES">NAMES AND TITLES</a>
          section.
        <div class="Pp"></div>
        Examples are:
        <div class="Pp"></div>
        <div class="Bd" style="margin-left: 5.00ex;">
        <pre class="Li">#(sysctl vm.loadavg) 
#[fg=yellow,bold]#(apm -l)%%#[default] [#S]
        </pre>
        </div>
        <div class="Pp"></div>
        The default is ‘<code class="Li">[#S] </code>’.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-left-length"><b class="Ic" title="Ic" id="status-left-length">status-left-length</b></a>
        <var class="Ar" title="Ar">length</var></dt>
      <dd class="It-tag">Set the maximum <var class="Ar" title="Ar">length</var>
          of the left component of the status line. The default is 10.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-left-style"><b class="Ic" title="Ic" id="status-left-style">status-left-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set the style of the left part of the status line. For
          how to specify <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-position"><b class="Ic" title="Ic" id="status-position">status-position</b></a>
        [<span class="Op"><b class="Ic" title="Ic">top</b> |
        <b class="Ic" title="Ic">bottom</b></span>]</dt>
      <dd class="It-tag">Set the position of the status line.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-right"><b class="Ic" title="Ic" id="status-right">status-right</b></a>
        <var class="Ar" title="Ar">string</var></dt>
      <dd class="It-tag">Display <var class="Ar" title="Ar">string</var> to the
          right of the status line. By default, the current pane title in double
          quotes, the date and the time are shown. As with
          <b class="Ic" title="Ic">status-left</b>,
          <var class="Ar" title="Ar">string</var> will be passed to
          <a class="Xr" title="Xr" href="http://man.openbsd.org/strftime.3">strftime(3)</a> and
          character pairs are replaced.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-right-length"><b class="Ic" title="Ic" id="status-right-length">status-right-length</b></a>
        <var class="Ar" title="Ar">length</var></dt>
      <dd class="It-tag">Set the maximum <var class="Ar" title="Ar">length</var>
          of the right component of the status line. The default is 40.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-right-style"><b class="Ic" title="Ic" id="status-right-style">status-right-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set the style of the right part of the status line. For
          how to specify <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#status-style"><b class="Ic" title="Ic" id="status-style">status-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set status line style. For how to specify
          <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#update-environment[]"><b class="Ic" title="Ic" id="update-environment[]">update-environment[]</b></a>
        <var class="Ar" title="Ar">variable</var></dt>
      <dd class="It-tag">Set list of environment variables to be copied into the
          session environment when a new session is created or an existing
          session is attached. Any variables that do not exist in the source
          environment are set to be removed from the session environment (as if
          <b class="Fl" title="Fl">-r</b> was given to the
          <b class="Ic" title="Ic">set-environment</b> command).</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#user-keys[]"><b class="Ic" title="Ic" id="user-keys[]">user-keys[]</b></a>
        <var class="Ar" title="Ar">key</var></dt>
      <dd class="It-tag">Set list of user-defined key escape sequences. Each
          item is associated with a key named
          ‘<code class="Li">User0</code>’,
          ‘<code class="Li">User1</code>’, and so on.
        <div class="Pp"></div>
        For example:
        <div class="Pp"></div>
        <div class="Bd" style="margin-left: 5.00ex;">
        <pre class="Li">set -s user-keys[0] "\e[5;30012~" 
bind User0 resize-pane -L 3
        </pre>
        </div>
      </dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#visual-activity"><b class="Ic" title="Ic" id="visual-activity">visual-activity</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b> |
        <b class="Ic" title="Ic">both</b></span>]</dt>
      <dd class="It-tag">If on, display a message instead of sending a bell when
          activity occurs in a window for which the
          <b class="Ic" title="Ic">monitor-activity</b> window option is
          enabled. If set to both, a bell and a message are produced.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#visual-bell"><b class="Ic" title="Ic" id="visual-bell">visual-bell</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b> |
        <b class="Ic" title="Ic">both</b></span>]</dt>
      <dd class="It-tag">If on, a message is shown on a bell in a window for
          which the <b class="Ic" title="Ic">monitor-bell</b> window option is
          enabled instead of it being passed through to the terminal (which
          normally makes a sound). If set to both, a bell and a message are
          produced. Also see the <b class="Ic" title="Ic">bell-action</b>
          option.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#visual-silence"><b class="Ic" title="Ic" id="visual-silence">visual-silence</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b> |
        <b class="Ic" title="Ic">both</b></span>]</dt>
      <dd class="It-tag">If <b class="Ic" title="Ic">monitor-silence</b> is
          enabled, prints a message after the interval has expired on a given
          window instead of sending a bell. If set to both, a bell and a message
          are produced.</dd>
      <dt class="It-tag">&nbsp;</dt>
      <dd class="It-tag">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#word-separators"><b class="Ic" title="Ic" id="word-separators">word-separators</b></a>
        <var class="Ar" title="Ar">string</var></dt>
      <dd class="It-tag">Sets the session's conception of what characters are
          considered word separators, for the purposes of the next and previous
          word commands in copy mode. The default is
          ‘<code class="Li">&nbsp;-_@</code>’.</dd>
    </dl>
  </dd>
  <dt class="It-tag">&nbsp;</dt>
  <dd class="It-tag">&nbsp;</dd>
  <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#set-window-option"><b class="Ic" title="Ic" id="set-window-option">set-window-option</b></a>
    [<span class="Op"><b class="Fl" title="Fl">-aFgoqu</b></span>]
    [<span class="Op"><b class="Fl" title="Fl">-t</b>
    <var class="Ar" title="Ar">target-window</var></span>]
    <var class="Ar" title="Ar">option</var>
    <var class="Ar" title="Ar">value</var></dt>
  <dd class="It-tag">
    <div class="D1">(alias: <b class="Ic" title="Ic">setw</b>)</div>
    Set a window option. The <b class="Fl" title="Fl">-a</b>,
      <b class="Fl" title="Fl">-F</b>, <b class="Fl" title="Fl">-g</b>,
      <b class="Fl" title="Fl">-o</b>, <b class="Fl" title="Fl">-q</b> and
      <b class="Fl" title="Fl">-u</b> flags work similarly to the
      <b class="Ic" title="Ic">set-option</b> command.
    <div class="Pp"></div>
    Supported window options are:
    <div class="Pp"></div>
    <dl class="Bl-tag Bl-compact">
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#aggressive-resize"><b class="Ic" title="Ic" id="aggressive-resize">aggressive-resize</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Aggressively resize the chosen window. This means that
          <b class="Nm" title="Nm">tmux</b> will resize the window to the size
          of the smallest session for which it is the current window, rather
          than the smallest session to which it is attached. The window may
          resize when the current window is changed on another sessions; this
          option is good for full-screen programs which support
          <code class="Dv" title="Dv">SIGWINCH</code> and poor for interactive
          programs such as shells.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#allow-rename"><b class="Ic" title="Ic" id="allow-rename">allow-rename</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Allow programs to change the window name using a
          terminal escape sequence (\ek...\e\\). The default is off.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#alternate-screen"><b class="Ic" title="Ic" id="alternate-screen">alternate-screen</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">This option configures whether programs running inside
          <b class="Nm" title="Nm">tmux</b> may use the terminal alternate
          screen feature, which allows the <i class="Em" title="Em">smcup</i>
          and <i class="Em" title="Em">rmcup</i>
          <a class="Xr" title="Xr" href="http://man.openbsd.org/terminfo.5">terminfo(5)</a>
          capabilities. The alternate screen feature preserves the contents of
          the window when an interactive application starts and restores it on
          exit, so that any output visible before the application starts
          reappears unchanged after it exits. The default is on.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#automatic-rename"><b class="Ic" title="Ic" id="automatic-rename">automatic-rename</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Control automatic window renaming. When this setting is
          enabled, <b class="Nm" title="Nm">tmux</b> will rename the window
          automatically using the format specified by
          <b class="Ic" title="Ic">automatic-rename-format</b>. This flag is
          automatically disabled for an individual window when a name is
          specified at creation with <b class="Ic" title="Ic">new-window</b> or
          <b class="Ic" title="Ic">new-session</b>, or later with
          <b class="Ic" title="Ic">rename-window</b>, or with a terminal escape
          sequence. It may be switched off globally with:
        <div class="Pp"></div>
        <div class="Bd" style="margin-left: 5.00ex;">
        <pre class="Li">set-window-option -g automatic-rename off
        </pre>
        </div>
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#automatic-rename-format"><b class="Ic" title="Ic" id="automatic-rename-format">automatic-rename-format</b></a>
        <var class="Ar" title="Ar">format</var></dt>
      <dd class="It-tag">The format (see
          <a class="Sx" title="Sx" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#FORMATS">FORMATS</a>) used when the
          <b class="Ic" title="Ic">automatic-rename</b> option is enabled.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#clock-mode-colour"><b class="Ic" title="Ic" id="clock-mode-colour">clock-mode-colour</b></a>
        <var class="Ar" title="Ar">colour</var></dt>
      <dd class="It-tag">Set clock colour.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#clock-mode-style"><b class="Ic" title="Ic" id="clock-mode-style">clock-mode-style</b></a>
        [<span class="Op"><b class="Ic" title="Ic">12</b> |
        <b class="Ic" title="Ic">24</b></span>]</dt>
      <dd class="It-tag">Set clock hour format.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#force-height"><b class="Ic" title="Ic" id="force-height">force-height</b></a>
        <var class="Ar" title="Ar">height</var></dt>
      <dd class="It-tag" style="width: auto;">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#force-width"><b class="Ic" title="Ic" id="force-width">force-width</b></a>
        <var class="Ar" title="Ar">width</var></dt>
      <dd class="It-tag">Prevent <b class="Nm" title="Nm">tmux</b> from resizing
          a window to greater than <var class="Ar" title="Ar">width</var> or
          <var class="Ar" title="Ar">height</var>. A value of zero restores the
          default unlimited setting.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#main-pane-height"><b class="Ic" title="Ic" id="main-pane-height">main-pane-height</b></a>
        <var class="Ar" title="Ar">height</var></dt>
      <dd class="It-tag" style="width: auto;">&nbsp;</dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#main-pane-width"><b class="Ic" title="Ic" id="main-pane-width">main-pane-width</b></a>
        <var class="Ar" title="Ar">width</var></dt>
      <dd class="It-tag">Set the width or height of the main (left or top) pane
          in the <b class="Ic" title="Ic">main-horizontal</b> or
          <b class="Ic" title="Ic">main-vertical</b> layouts.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#mode-keys"><b class="Ic" title="Ic" id="mode-keys">mode-keys</b></a>
        [<span class="Op"><b class="Ic" title="Ic">vi</b> |
        <b class="Ic" title="Ic">emacs</b></span>]</dt>
      <dd class="It-tag">Use vi or emacs-style key bindings in copy mode. The
          default is emacs, unless <code class="Ev" title="Ev">VISUAL</code> or
          <code class="Ev" title="Ev">EDITOR</code> contains
          ‘<code class="Li">vi</code>’.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#mode-style"><b class="Ic" title="Ic" id="mode-style">mode-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set window modes style. For how to specify
          <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#monitor-activity"><b class="Ic" title="Ic" id="monitor-activity">monitor-activity</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Monitor for activity in the window. Windows with
          activity are highlighted in the status line.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#monitor-bell"><b class="Ic" title="Ic" id="monitor-bell">monitor-bell</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Monitor for a bell in the window. Windows with a bell
          are highlighted in the status line.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#monitor-silence"><b class="Ic" title="Ic" id="monitor-silence">monitor-silence</b></a>
        [<span class="Op"><b class="Ic" title="Ic">interval</b></span>]</dt>
      <dd class="It-tag">Monitor for silence (no activity) in the window within
          <b class="Ic" title="Ic">interval</b> seconds. Windows that have been
          silent for the interval are highlighted in the status line. An
          interval of zero disables the monitoring.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#other-pane-height"><b class="Ic" title="Ic" id="other-pane-height">other-pane-height</b></a>
        <var class="Ar" title="Ar">height</var></dt>
      <dd class="It-tag">Set the height of the other panes (not the main pane)
          in the <b class="Ic" title="Ic">main-horizontal</b> layout. If this
          option is set to 0 (the default), it will have no effect. If both the
          <b class="Ic" title="Ic">main-pane-height</b> and
          <b class="Ic" title="Ic">other-pane-height</b> options are set, the
          main pane will grow taller to make the other panes the specified
          height, but will never shrink to do so.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#other-pane-width"><b class="Ic" title="Ic" id="other-pane-width">other-pane-width</b></a>
        <var class="Ar" title="Ar">width</var></dt>
      <dd class="It-tag">Like <b class="Ic" title="Ic">other-pane-height</b>,
          but set the width of other panes in the
          <b class="Ic" title="Ic">main-vertical</b> layout.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pane-active-border-style"><b class="Ic" title="Ic" id="pane-active-border-style">pane-active-border-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set the pane border style for the currently active
          pane. For how to specify <var class="Ar" title="Ar">style</var>, see
          the <b class="Ic" title="Ic">message-command-style</b> option.
          Attributes are ignored.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pane-base-index"><b class="Ic" title="Ic" id="pane-base-index">pane-base-index</b></a>
        <var class="Ar" title="Ar">index</var></dt>
      <dd class="It-tag">Like <b class="Ic" title="Ic">base-index</b>, but set
          the starting index for pane numbers.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pane-border-format"><b class="Ic" title="Ic" id="pane-border-format">pane-border-format</b></a>
        <var class="Ar" title="Ar">format</var></dt>
      <dd class="It-tag">Set the text shown in pane border status lines.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pane-border-status"><b class="Ic" title="Ic" id="pane-border-status">pane-border-status</b></a>
        [<span class="Op"><b class="Ic" title="Ic">off</b> |
        <b class="Ic" title="Ic">top</b> |
        <b class="Ic" title="Ic">bottom</b></span>]</dt>
      <dd class="It-tag">Turn pane border status lines off or set their
          position.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#pane-border-style"><b class="Ic" title="Ic" id="pane-border-style">pane-border-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set the pane border style for panes aside from the
          active pane. For how to specify
          <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option. Attributes
          are ignored.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#remain-on-exit"><b class="Ic" title="Ic" id="remain-on-exit">remain-on-exit</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">A window with this flag set is not destroyed when the
          program running in it exits. The window may be reactivated with the
          <b class="Ic" title="Ic">respawn-window</b> command.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#synchronize-panes"><b class="Ic" title="Ic" id="synchronize-panes">synchronize-panes</b></a>
        [<span class="Op"><b class="Ic" title="Ic">on</b> |
        <b class="Ic" title="Ic">off</b></span>]</dt>
      <dd class="It-tag">Duplicate input to any pane to all other panes in the
          same window (only for panes that are not in any special mode).
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#window-active-style"><b class="Ic" title="Ic" id="window-active-style">window-active-style</b></a>
        <var class="Ar" title="Ar">style</var></dt>
      <dd class="It-tag">Set the style for the window's active pane. For how to
          specify <var class="Ar" title="Ar">style</var>, see the
          <b class="Ic" title="Ic">message-command-style</b> option.
        <div class="Pp"></div>
      </dd>
      <dt class="It-tag"><a class="selflink" href="http://man.openbsd.org/OpenBSD-current/man1/tmux.1#window-status-activity-style"><b class="Ic" title="Ic" id="window-status-activity-style">window-status-activity-style</b></a>
        </dt></dl></dd></dl></div></body></html>
